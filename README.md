<? PHP
/ **
* @package     Joomla.Site
 *
* @copyright   Copyright (C) 2005 - 2018 Open Source Matters, Inc. Все права защищены.
* @license     GNU General Public License версия 2 или более поздняя; см. LICENSE.txt
 * /
/ **
 * Определите минимальную поддерживаемую версию PHP приложения как константу, чтобы на нее можно было ссылаться в приложении.
 * /
define ( ' JOOMLA_MINIMUM_PHP ' , ' 5.3.10 ' );
if ( version_compare ( PHP_VERSION , JOOMLA_MINIMUM_PHP , ' < ' ))
{
	die ( ' Ваш хост должен использовать PHP '  .  JOOMLA_MINIMUM_PHP  .  ' или новее, чтобы запустить эту версию Joomla! ' );
}
// Сохраняет время начала и использование памяти.
$ startTime  =  microtime ( 1 );
$ startMem   =  memory_get_usage ();
/ **
 * Константа, которая проверяется во включенных файлах, чтобы предотвратить прямой доступ.
 * define () используется в папке установки вместо «const», чтобы не выдавать ошибку для PHP 5.2 и ниже
 * /
define ( ' _JEXEC ' , 1 );
если ( file_exists ( __DIR__  .  ' /defines.php ' ))
{
	include_once  __DIR__  .  ' /defines.php ' ;
}
если ( ! определено ( ' _JDEFINES ' ))
{
	определить ( ' JPATH_BASE ' , __DIR__ );
	require_once  JPATH_BASE  .  ' /include/defines.php ' ;
}
require_once  JPATH_BASE  .  ' /include/framework.php ' ;
// Установить время запуска профилировщика и использование памяти и пометить afterLoad в профилировщике.
JDEBUG ? JProfiler :: getInstance ( ' Приложение ' ) -> setStart ( $ startTime , $ startMem ) -> mark ( ' afterLoad ' ): null ;
// Создание приложения.
$ app  =  JFactory :: getApplication ( ' site ' );
// Выполнить приложение.
$ app -> execute ();
