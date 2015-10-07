nginx
==============================

fastcgi
------------------------------
fastcgi_params 一定要加上 ::

  fastcgi_param	SCRIPT_FILENAME		$request_filename;

tengine 使用 fastcgi.conf ，不要用 fastcgi_params

