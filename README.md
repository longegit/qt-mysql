下载qt源码，
进入$QtDir/src/plugins/sqldrivers/mysql/
修改mysql.pro文件，注释掉QMAKE_USE += mysql这行
把上级目录定config.pri文件复制一份改成 qtsqldrivers-config.pri
执行/Users/apple/Qt5.13.0/5.13.0/clang_64/bin/qmake "INCLUDEPATH+=/usr/local/mysql/include" "LIBS+=-L/usr/local/mysql/lib -lmysqlclient" mysql.pro
make
make install

进入 Qt5.13.0/5.13.0/clang_64/plugins/sqldrivers目录
otool -L libqsqlmysql.dylib 查看库定引用路径
install_name_tool -change libmysqlclient.21.dylib /usr/local/mysql/lib/libmysqlclient.21.dylib libqsqlmysql.dylib
install_name_tool -add_rpath /usr/local/mysql/lib libqsqlmysql.dylib
如果提示rpath找不到的问题，试试上面的命令。
