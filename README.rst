DataTable
=========

Lib para crear tablas html con el resultado de una consulta ActiveRecord

Ejemplo de Uso
==============

::

	//en el controlador
	$this->menus = Load::model("menus")->find();

	//en la vista

	//pasamos el resultado de la consulta al constructor de la clase
	$dt = new DataTable($menus);

	//creamos las cabeceras de las columnas

	//podemos pasar cualquier html en las columnas
	$dt->addHeaders(Form::check('seleccionar_todos', 'todos', NULL, FALSE));
	//cada vez que llamemos a addHeaders se van a agregar columnas a la tabla.
	$dt->addHeaders('id', 'Texto a Mostrar', 'Menu Padre');
	$dt->addHeaders('Recurso al que Accede', 'URL', 'Posición');
	$dt->addHeaders('Estado', 'Editar', 'Eliminar');

	//agregamos los campos del modelo a usar

	$dt->check('menu_id'); //creamos un checkbox con name="menu_id[]"

	//agregamos los campos del modelo de donde sacaremos los valores.
	$dt->addFields('id', 'nombre', 'padre', 'recurso', 'url', 'posicion');
	//tambien podemos especificar nombres de metodos, por defecto
	//busca si el metodo existe, si es así lo llama y muestra el resultado
	//sino existe el metodo, llama al atributo directamente.

	//crea un link con una imagen
	$dt->imgLink('figuras/circulo_rojo.png|figuras/circulo_verde.png',
	        'admin/menu/activar|admin/menu/desactivar', '', 'activo');
	$dt->imgLink('figuras/editar.png', 'admin/menu/editar');

	//crea un link con una imagen y muestra un enlace de confirmación
	$dt->imgLinkConfirm('figuras/eliminar.png', 'admin/menu/eliminar', '',
	        '¿Realmente desea Eliminar El Menu ?');


	//genera la tabla html
	echo $dt->render('class="table table-bordered table-striped"');


