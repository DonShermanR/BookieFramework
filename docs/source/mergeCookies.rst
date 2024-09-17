Manual de Usuario para Database Merger GUI
==========================================

Introducción
------------

**Database Merger** es una aplicación de interfaz gráfica de usuario (GUI) desarrollada en Python utilizando PyQt5. Permite a los usuarios seleccionar múltiples archivos de base de datos SQLite y combinarlos en una única base de datos de destino. Este manual detalla cómo utilizar la aplicación.

Requisitos
----------

Asegúrese de tener instalados los siguientes elementos:

- Python 3.x
- PyQt5
- SQLite

Para instalar PyQt5, ejecute el siguiente comando:

.. code-block:: bash

    pip install PyQt5

Iniciar la Aplicación
---------------------

Para iniciar la aplicación, ejecute el siguiente script en su terminal:

.. code-block:: bash

    python db_merger_gui.py

Ventana Principal
-----------------

Al abrir la aplicación, verá una ventana con los siguientes elementos:

- **Seleccionar Bases de Datos**: Un botón que permite seleccionar las bases de datos SQLite que se desean combinar.
- **Seleccionar Base de Datos Destino**: Un botón que permite seleccionar o crear la base de datos donde se guardarán los datos combinados.
- **Combinar Bases de Datos**: Inicia el proceso de combinación de bases de datos.
- **Lista de Archivos**: Muestra los nombres de las bases de datos seleccionadas.
- **Etiqueta de Estado**: Muestra información sobre las bases de datos seleccionadas.
- **Botón Regresar**: Cierra la aplicación.

Pasos para Usar la Aplicación
-----------------------------

1. **Seleccionar Bases de Datos Fuente**

   Haga clic en el botón **Seleccionar Bases de Datos**. Se abrirá un cuadro de diálogo donde podrá elegir las bases de datos SQLite que desea combinar.
   Las bases seleccionadas aparecerán en la lista de archivos.

.. code-block:: python

    def select_source_files(self):
        files, _ = QFileDialog.getOpenFileNames(self, "Seleccionar Bases de Datos", "", "All Files (*)")
        if files:
            self.source_dbs = files
            self.file_list.clear()
            self.file_list.addItems([os.path.basename(f) for f in files])
            self.update_status()

2. **Seleccionar Base de Datos Destino**

   Haga clic en **Seleccionar Base de Datos Destino** para elegir o crear una base de datos donde se guardarán los datos combinados.

.. code-block:: python

    def select_destination_database(self):
        self.destination_db, _ = QFileDialog.getSaveFileName(self, "Seleccionar Base de Datos Destino", "", "SQLite Database (*.db)")
        if self.destination_db:
            self.update_status()

3. **Combinar Bases de Datos**

   Haga clic en el botón **Combinar Bases de Datos** para iniciar el proceso de fusión. Se copiarán todas las tablas y datos de las bases de datos fuente a la base de datos de destino.

.. code-block:: python

    def merge_databases(self):
        if not self.source_dbs or not hasattr(self, 'destination_db'):
            QMessageBox.warning(self, "Advertencia", "Seleccione las bases de datos fuente y una base de datos destino.")
            return

        try:
            self.merge_databases_logic(self.source_dbs, self.destination_db)
            QMessageBox.information(self, "Éxito", "Las bases de datos se han combinado exitosamente.")
        except Exception as e:
            QMessageBox.critical(self, "Error", f"Ocurrió un error al combinar las bases de datos: {str(e)}")

Detalles Técnicos
-----------------

El código que combina las bases de datos fuente en la base de datos destino sigue este flujo:

1. Abre la base de datos destino.
2. Itera a través de las bases de datos fuente.
3. Copia las tablas y sus datos a la base de datos destino.

.. code-block:: python

    def merge_databases_logic(self, source_dbs, destination_db):
        dest_conn = sqlite3.connect(destination_db)
        dest_cursor = dest_conn.cursor()

        for db in source_dbs:
            try:
                source_conn = sqlite3.connect(db)
                source_cursor = source_conn.cursor()

                source_cursor.execute("SELECT name FROM sqlite_master WHERE type='table';")
                tables = source_cursor.fetchall()

                for table in tables:
                    table_name = table[0]
                    source_cursor.execute(f"PRAGMA table_info({table_name})")
                    columns_info = source_cursor.fetchall()

                    column_defs = ", ".join([f"{col[1]} {col[2]}" for col in columns_info])
                    dest_cursor.execute(f"CREATE TABLE IF NOT EXISTS {table_name} ({column_defs})")

                    source_cursor.execute(f"SELECT * FROM {table_name}")
                    rows = source_cursor.fetchall()
                    
                    if rows:
                        placeholders = ", ".join(["?" for _ in columns_info])
                        dest_cursor.executemany(f"INSERT OR IGNORE INTO {table_name} VALUES ({placeholders})", rows)

                source_conn.close()
                dest_conn.commit()
            except sqlite3.Error as e:
                print(f"Error processing {db}: {str(e)}")

        dest_conn.close()

Salir de la Aplicación
----------------------

El botón **Regresar** cierra la aplicación:

.. code-block:: python

    def go_back(self):
        self.close()

