# librcsc 的依赖

对于本项目，需要Boost库。
- 在 Ubuntu 24.04 是`sudo apt install libboost-all-dev`
- 在 Windows MSYS2 UCRT64 是`pacman -S mingw-w64-ucrt-x86_64-boost`

# CMake 方式构建

CMake方式在Ubuntu 22.04失效，但在Ubuntu 24.04生效，是因为宏定义的问题。但是autotools在两个版本都有效。但是还是推荐使用Ubuntu 24.04构建

```sh
rm -r build
cmake -S . -B build -G "Unix Makefiles" -DCMAKE_BUILD_TYPE=Release
cmake --build build -j
```

如果你需要构建 example 目录下的示例程序，请在配置时加上 `-DBUILD_EXAMPLE=ON`。

# CMake 方式安装

- 安装到系统默认路径（通常是`/usr/local`，需要sudo）
```sh
sudo cmake --install build
```

现在，可以用`pkg-config --modversion librcsc`来查看这个库的版本号。如果有版本号输出，说明安装已被系统识别。

卸载命令如下
```sh
sudo cmake --build build --target uninstall
```

## CMake 方式安装（自定义位置）

如果想要安装到其他位置，先重新配置，对于helios-base支持自动发现`~/local`和`~/.local`两种路径，其他路径需要手动指定库为位置
```sh
rm -r build
cmake -S . -B build-local -G "Unix Makefiles" -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX="$HOME/local"
cmake --build build -j
sudo cmake --install build
pkg-config --modversion librcsc
```

# 附录

autotool 方式已经被我淘汰！这个方法对大家上手有点难，且不优雅！

## autotool 方式构建

- https://github.com/hunspell/hunspell/issues/728
- https://stackoverflow.com/questions/62662905/inig-status-error-cannot-find-input-file-makefile

Linux下编译需要确保文件都是LF格式`dos2unix ./*.*`

在根目录执行命令以构建库：
```
./bootstrap
./configure --disable-unit-test
make -j
```

## autotool 方式安装

如果想要安装到其他位置，先重新配置，对于helios-base支持`~/local`和`~/.local`两种路径
```sh
./configure --prefix=$HOME/local
make -j
```

构建完成后，你可以用`make install`把库安装到它的默认安装位置。

现在，可以用`pkg-config --modversion librcsc`来查看这个库的版本号。如果有版本号输出，说明安装已被系统识别。

这个库也可以轻而易举地用`make uninstall`卸载。

Ubuntu会把它安装在`/usr/local`下。

<details>
<summary>Ubuntu 24.04示例输出</summary>

```
enoch@DESKTOP-FLOWX13:/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc$ sudo make install
Making install in rcsc
make[1]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc”
Making install in util
make[2]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/util”
make[3]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/util”
make[3]: 对“install-exec-am”无需做任何事。
make[3]: 对“install-data-am”无需做任何事。
make[3]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/util”
make[2]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/util”
Making install in geom
make[2]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/geom”
Making install in triangle
make[3]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/geom/triangle”
make[4]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/geom/triangle”
make[4]: 对“install-exec-am”无需做任何事。
make[4]: 对“install-data-am”无需做任何事。
make[4]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/geom/triangle”
make[3]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/geom/triangle”
Making install in .
make[3]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/geom”
make[4]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/geom”
make[4]: 对“install-exec-am”无需做任何事。
 /usr/bin/mkdir -p '/usr/local/include/rcsc/geom'
 /usr/bin/install -c -m 644 angle_deg.h circle_2d.h composite_region_2d.h convex_hull.h delaunay_triangulation.h line_2d.h matrix_2d.h polygon_2d.h ray_2d.h rect_2d.h region_2d.h sector_2d.h size_2d.h segment_2d.h triangle_2d.h triangulation.h vector_2d.h voronoi_diagram.h voronoi_diagram_triangle.h '/usr/local/include/rcsc/geom'
make[4]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/geom”
make[3]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/geom”
make[2]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/geom”
Making install in gz
make[2]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/gz”
make[3]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/gz”
make[3]: 对“install-exec-am”无需做任何事。
 /usr/bin/mkdir -p '/usr/local/include/rcsc/gz'
 /usr/bin/install -c -m 644 gzcompressor.h gzfstream.h gzfilterstream.h '/usr/local/include/rcsc/gz'
make[3]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/gz”
make[2]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/gz”
Making install in param
make[2]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/param”
make[3]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/param”
make[3]: 对“install-exec-am”无需做任何事。
 /usr/bin/mkdir -p '/usr/local/include/rcsc/param'
 /usr/bin/install -c -m 644 cmd_line_parser.h conf_file_parser.h param_map.h param_parser.h rcss_param_parser.h '/usr/local/include/rcsc/param'
make[3]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/param”
make[2]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/param”
Making install in rcg
make[2]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/rcg”
make[3]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/rcg”
make[3]: 对“install-exec-am”无需做任何事。
 /usr/bin/mkdir -p '/usr/local/include/rcsc/rcg'
 /usr/bin/install -c -m 644 handler.h parser.h parser_v1.h parser_v2.h parser_v3.h parser_v4.h parser_simdjson.h serializer.h serializer_v1.h serializer_v2.h serializer_v3.h serializer_v4.h serializer_v5.h serializer_v6.h serializer_json.h types.h util.h '/usr/local/include/rcsc/rcg'
make[3]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/rcg”
make[2]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/rcg”
Making install in net
make[2]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/net”
make[3]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/net”
make[3]: 对“install-exec-am”无需做任何事。
 /usr/bin/mkdir -p '/usr/local/include/rcsc/net'
 /usr/bin/install -c -m 644 abstract_socket.h host_address.h udp_socket.h tcp_socket.h '/usr/local/include/rcsc/net'
make[3]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/net”
make[2]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/net”
Making install in time
make[2]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/time”
make[3]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/time”
make[3]: 对“install-exec-am”无需做任何事。
 /usr/bin/mkdir -p '/usr/local/include/rcsc/time'
 /usr/bin/install -c -m 644 timer.h '/usr/local/include/rcsc/time'
make[3]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/time”
make[2]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/time”
Making install in ann
make[2]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/ann”
make[3]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/ann”
make[3]: 对“install-exec-am”无需做任何事。
 /usr/bin/mkdir -p '/usr/local/include/rcsc/ann'
 /usr/bin/install -c -m 644 bpn1.h ngnet.h rbf.h sirm.h sirms_model.h '/usr/local/include/rcsc/ann'
make[3]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/ann”
make[2]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/ann”
Making install in clang
make[2]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/clang”
make[3]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/clang”
make[3]: 对“install-exec-am”无需做任何事。
 /usr/bin/mkdir -p '/usr/local/include/rcsc/clang'
 /usr/bin/install -c -m 644 clang_action.h clang_condition.h clang_directive.h clang_info_message.h clang_message.h clang_parser.h clang_token.h clang_unum.h clang.h types.h '/usr/local/include/rcsc/clang'
make[3]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/clang”
make[2]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/clang”
Making install in formation
make[2]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/formation”
make[3]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/formation”
make[3]: 对“install-exec-am”无需做任何事。
 /usr/bin/mkdir -p '/usr/local/include/rcsc/formation'
 /usr/bin/install -c -m 644 formation.h formation_data.h formation_parser.h formation_parser_csv.h formation_parser_json.h formation_parser_static.h formation_parser_v1.h formation_parser_v2.h formation_parser_v3.h formation_dt.h formation_static.h role_type.h '/usr/local/include/rcsc/formation'
make[3]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/formation”
make[2]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/formation”
Making install in color
make[2]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/color”
make[3]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/color”
make[3]: 对“install-exec-am”无需做任何事。
 /usr/bin/mkdir -p '/usr/local/include/rcsc/color'
 /usr/bin/install -c -m 644 rgb_color.h gradation_color_provider.h gray_scale_provider.h thermo_color_provider.h '/usr/local/include/rcsc/color'
make[3]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/color”
make[2]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/color”
Making install in common
make[2]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/common”
make[3]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/common”
make[3]: 对“install-exec-am”无需做任何事。
 /usr/bin/mkdir -p '/usr/local/include/rcsc/common'
 /usr/bin/install -c -m 644 abstract_client.h audio_codec.h audio_memory.h audio_message.h free_message_parser.h freeform_message.h freeform_message_parser.h logger.h offline_client.h online_client.h player_param.h player_type.h say_message.h say_message_parser.h server_param.h soccer_agent.h stamina_model.h team_graphic.h '/usr/local/include/rcsc/common'
make[3]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/common”
make[2]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/common”
Making install in monitor
make[2]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/monitor”
make[3]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/monitor”
make[3]: 对“install-exec-am”无需做任何事。
 /usr/bin/mkdir -p '/usr/local/include/rcsc/monitor'
 /usr/bin/install -c -m 644 monitor_command.h '/usr/local/include/rcsc/monitor'
make[3]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/monitor”
make[2]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/monitor”
Making install in player
make[2]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/player”
make[3]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/player”
make[3]: 对“install-exec-am”无需做任何事。
 /usr/bin/mkdir -p '/usr/local/include/rcsc/player'
 /usr/bin/install -c -m 644 abstract_player_object.h action_effector.h audio_sensor.h ball_object.h body_sensor.h debug_client.h free_message.h fullstate_sensor.h intercept.h intercept_simulator_player.h intercept_simulator_self.h intercept_simulator_self_v17.h intercept_table.h localization.h localization_default.h object_table.h penalty_kick_state.h player_command.h player_agent.h player_config.h player_evaluator.h player_object.h player_predicate.h player_state.h say_message_builder.h see_state.h self_object.h soccer_action.h soccer_intention.h view_area.h view_grid_map.h view_mode.h visual_sensor.h world_model.h '/usr/local/include/rcsc/player'
make[3]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/player”
make[2]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/player”
Making install in coach
make[2]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/coach”
make[3]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/coach”
make[3]: 对“install-exec-am”无需做任何事。
 /usr/bin/mkdir -p '/usr/local/include/rcsc/coach'
 /usr/bin/install -c -m 644 coach_agent.h coach_audio_sensor.h coach_ball_object.h coach_command.h coach_config.h coach_debug_client.h coach_intercept_predictor.h coach_player_object.h coach_visual_sensor.h coach_world_model.h coach_world_state.h player_type_analyzer.h '/usr/local/include/rcsc/coach'
make[3]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/coach”
make[2]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/coach”
Making install in trainer
make[2]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/trainer”
make[3]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/trainer”
make[3]: 对“install-exec-am”无需做任何事。
 /usr/bin/mkdir -p '/usr/local/include/rcsc/trainer'
 /usr/bin/install -c -m 644 trainer_agent.h trainer_command.h trainer_config.h '/usr/local/include/rcsc/trainer'
make[3]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/trainer”
make[2]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc/trainer”
Making install in .
make[2]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc”
make[3]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc”
 /usr/bin/mkdir -p '/usr/local/lib'
 /bin/bash ../libtool   --mode=install /usr/bin/install -c   librcsc.la '/usr/local/lib'
libtool: install: /usr/bin/install -c .libs/librcsc.so.19.0.0 /usr/local/lib/librcsc.so.19.0.0
libtool: install: (cd /usr/local/lib && { ln -s -f librcsc.so.19.0.0 librcsc.so.19 || { rm -f librcsc.so.19 && ln -s librcsc.so.19.0.0 librcsc.so.19; }; })
libtool: install: (cd /usr/local/lib && { ln -s -f librcsc.so.19.0.0 librcsc.so || { rm -f librcsc.so && ln -s librcsc.so.19.0.0 librcsc.so; }; })
libtool: install: /usr/bin/install -c .libs/librcsc.lai /usr/local/lib/librcsc.la
libtool: finish: PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin:/sbin" ldconfig -n /usr/local/lib
----------------------------------------------------------------------
Libraries have been installed in:
   /usr/local/lib

If you ever happen to want to link against installed libraries
in a given directory, LIBDIR, you must either use libtool, and
specify the full pathname of the library, or use the '-LLIBDIR'
flag during linking and do at least one of the following:
   - add LIBDIR to the 'LD_LIBRARY_PATH' environment variable
     during execution
   - add LIBDIR to the 'LD_RUN_PATH' environment variable
     during linking
   - use the '-Wl,-rpath -Wl,LIBDIR' linker flag
   - have your system administrator add LIBDIR to '/etc/ld.so.conf'

See any operating system documentation about shared libraries for
more information, such as the ld(1) and ld.so(8) manual pages.
----------------------------------------------------------------------
 /usr/bin/mkdir -p '/usr/local/include/rcsc'
 /usr/bin/install -c -m 644 types.h geom.h gz.h rcg.h factory.h game_mode.h game_time.h math_util.h random.h soccer_math.h timer.h version.h '/usr/local/include/rcsc'
make[3]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc”
make[2]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc”
make[1]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/rcsc”
Making install in example
make[1]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/example”
make[2]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/example”
make[2]: 对“install-exec-am”无需做任何事。
make[2]: 对“install-data-am”无需做任何事。
make[2]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/example”
make[1]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/example”
Making install in src
make[1]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/src”
make[2]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/src”
 /usr/bin/mkdir -p '/usr/local/bin'
  /bin/bash ../libtool   --mode=install /usr/bin/install -c rclmscheduler rclmtableprinter rcg2csv rcg2txt rcgrenameteam rcgresultprinter rcgreverse rcgvalidator rcgverconv rcgversion '/usr/local/bin'
libtool: install: /usr/bin/install -c rclmscheduler /usr/local/bin/rclmscheduler
libtool: install: /usr/bin/install -c rclmtableprinter /usr/local/bin/rclmtableprinter
libtool: install: /usr/bin/install -c .libs/rcg2csv /usr/local/bin/rcg2csv
libtool: install: /usr/bin/install -c .libs/rcg2txt /usr/local/bin/rcg2txt
libtool: install: /usr/bin/install -c .libs/rcgrenameteam /usr/local/bin/rcgrenameteam
libtool: install: /usr/bin/install -c .libs/rcgresultprinter /usr/local/bin/rcgresultprinter
libtool: install: /usr/bin/install -c .libs/rcgreverse /usr/local/bin/rcgreverse
libtool: install: /usr/bin/install -c .libs/rcgvalidator /usr/local/bin/rcgvalidator
libtool: install: /usr/bin/install -c .libs/rcgverconv /usr/local/bin/rcgverconv
libtool: install: /usr/bin/install -c .libs/rcgversion /usr/local/bin/rcgversion
make[2]: 对“install-data-am”无需做任何事。
make[2]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/src”
make[1]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc/src”
make[1]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc”
make[2]: 进入目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc”
 /usr/bin/mkdir -p '/usr/local/bin'
 /usr/bin/install -c librcsc-config librcscenv '/usr/local/bin'
 /usr/bin/mkdir -p '/usr/local/lib/pkgconfig'
 /usr/bin/install -c -m 644 librcsc.pc '/usr/local/lib/pkgconfig'
make[2]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc”
make[1]: 离开目录“/media/enoch/DISK/CODING/RoboCup2D/Touhoku2D/librcsc”
```

</details>

MSYS2-UCRT会把它安装在`/ucrt64/lib`和`/ucrt64/bin`和`/ucrt64/include`下。

<details>
<summary>MSYS2-UCRT64示例输出</summary>

```
enoch@DESKTOP-FLOWX13 UCRT64 /d/CODING/RoboCup2D/librcsc
$ make install
Making install in rcsc
make[1]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc'
Making install in util
make[2]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/util'
make[3]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/util'
make[3]: Nothing to be done for 'install-exec-am'.
make[3]: Nothing to be done for 'install-data-am'.
make[3]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/util'
make[2]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/util'
Making install in geom
make[2]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/geom'
Making install in triangle
make[3]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/geom/triangle'
make[4]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/geom/triangle'
make[4]: Nothing to be done for 'install-exec-am'.
make[4]: Nothing to be done for 'install-data-am'.
make[4]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/geom/triangle'
make[3]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/geom/triangle'
Making install in .
make[3]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/geom'
make[4]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/geom'
make[4]: Nothing to be done for 'install-exec-am'.
 /usr/bin/mkdir -p '/ucrt64/include/rcsc/geom'
 /usr/bin/install -c -m 644 angle_deg.h circle_2d.h composite_region_2d.h convex_hull.h delaunay_triangulation.h line_2d.h matrix_2d.h polygon_2d.h ray_2d.h rect_2d.h region_2d.h sector_2d.h size_2d.h segment_2d.h triangle_2d.h triangulation.h vector_2d.h voronoi_diagram.h voronoi_diagram_triangle.h '/ucrt64/include/rcsc/geom'
make[4]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/geom'
make[3]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/geom'
make[2]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/geom'
Making install in gz
make[2]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/gz'
make[3]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/gz'
make[3]: Nothing to be done for 'install-exec-am'.
 /usr/bin/mkdir -p '/ucrt64/include/rcsc/gz'
 /usr/bin/install -c -m 644 gzcompressor.h gzfstream.h gzfilterstream.h '/ucrt64/include/rcsc/gz'
make[3]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/gz'
make[2]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/gz'
Making install in param
make[2]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/param'
make[3]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/param'
make[3]: Nothing to be done for 'install-exec-am'.
 /usr/bin/mkdir -p '/ucrt64/include/rcsc/param'
 /usr/bin/install -c -m 644 cmd_line_parser.h conf_file_parser.h param_map.h param_parser.h rcss_param_parser.h '/ucrt64/include/rcsc/param'
make[3]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/param'
make[2]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/param'
Making install in rcg
make[2]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/rcg'
make[3]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/rcg'
make[3]: Nothing to be done for 'install-exec-am'.
 /usr/bin/mkdir -p '/ucrt64/include/rcsc/rcg'
 /usr/bin/install -c -m 644 handler.h parser.h parser_v1.h parser_v2.h parser_v3.h parser_v4.h parser_simdjson.h serializer.h serializer_v1.h serializer_v2.h serializer_v3.h serializer_v4.h serializer_v5.h serializer_v6.h serializer_json.h types.h util.h '/ucrt64/include/rcsc/rcg'
make[3]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/rcg'
make[2]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/rcg'
Making install in net
make[2]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/net'
make[3]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/net'
make[3]: Nothing to be done for 'install-exec-am'.
 /usr/bin/mkdir -p '/ucrt64/include/rcsc/net'
 /usr/bin/install -c -m 644 abstract_socket.h host_address.h udp_socket.h tcp_socket.h '/ucrt64/include/rcsc/net'
make[3]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/net'
make[2]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/net'
Making install in time
make[2]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/time'
make[3]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/time'
make[3]: Nothing to be done for 'install-exec-am'.
 /usr/bin/mkdir -p '/ucrt64/include/rcsc/time'
 /usr/bin/install -c -m 644 timer.h '/ucrt64/include/rcsc/time'
make[3]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/time'
make[2]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/time'
Making install in ann
make[2]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/ann'
make[3]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/ann'
make[3]: Nothing to be done for 'install-exec-am'.
 /usr/bin/mkdir -p '/ucrt64/include/rcsc/ann'
 /usr/bin/install -c -m 644 bpn1.h ngnet.h rbf.h sirm.h sirms_model.h '/ucrt64/include/rcsc/ann'
make[3]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/ann'
make[2]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/ann'
Making install in clang
make[2]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/clang'
make[3]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/clang'
make[3]: Nothing to be done for 'install-exec-am'.
 /usr/bin/mkdir -p '/ucrt64/include/rcsc/clang'
 /usr/bin/install -c -m 644 clang_action.h clang_condition.h clang_directive.h clang_info_message.h clang_message.h clang_parser.h clang_token.h clang_unum.h clang.h types.h '/ucrt64/include/rcsc/clang'
make[3]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/clang'
make[2]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/clang'
Making install in formation
make[2]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/formation'
make[3]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/formation'
make[3]: Nothing to be done for 'install-exec-am'.
 /usr/bin/mkdir -p '/ucrt64/include/rcsc/formation'
 /usr/bin/install -c -m 644 formation.h formation_data.h formation_parser.h formation_parser_csv.h formation_parser_json.h formation_parser_static.h formation_parser_v1.h formation_parser_v2.h formation_parser_v3.h formation_dt.h formation_static.h role_type.h '/ucrt64/include/rcsc/formation'
make[3]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/formation'
make[2]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/formation'
Making install in color
make[2]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/color'
make[3]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/color'
make[3]: Nothing to be done for 'install-exec-am'.
 /usr/bin/mkdir -p '/ucrt64/include/rcsc/color'
 /usr/bin/install -c -m 644 rgb_color.h gradation_color_provider.h gray_scale_provider.h thermo_color_provider.h '/ucrt64/include/rcsc/color'
make[3]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/color'
make[2]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/color'
Making install in common
make[2]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/common'
make[3]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/common'
make[3]: Nothing to be done for 'install-exec-am'.
 /usr/bin/mkdir -p '/ucrt64/include/rcsc/common'
 /usr/bin/install -c -m 644 abstract_client.h audio_codec.h audio_memory.h audio_message.h free_message_parser.h freeform_message.h freeform_message_parser.h logger.h offline_client.h online_client.h player_param.h player_type.h say_message.h say_message_parser.h server_param.h soccer_agent.h stamina_model.h team_graphic.h '/ucrt64/include/rcsc/common'
make[3]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/common'
make[2]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/common'
Making install in monitor
make[2]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/monitor'
make[3]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/monitor'
make[3]: Nothing to be done for 'install-exec-am'.
 /usr/bin/mkdir -p '/ucrt64/include/rcsc/monitor'
 /usr/bin/install -c -m 644 monitor_command.h '/ucrt64/include/rcsc/monitor'
make[3]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/monitor'
make[2]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/monitor'
Making install in player
make[2]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/player'
make[3]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/player'
make[3]: Nothing to be done for 'install-exec-am'.
 /usr/bin/mkdir -p '/ucrt64/include/rcsc/player'
 /usr/bin/install -c -m 644 abstract_player_object.h action_effector.h audio_sensor.h ball_object.h body_sensor.h debug_client.h free_message.h fullstate_sensor.h intercept.h intercept_simulator_player.h intercept_simulator_self.h intercept_simulator_self_v17.h intercept_table.h localization.h localization_default.h object_table.h penalty_kick_state.h player_command.h player_agent.h player_config.h player_evaluator.h player_object.h player_predicate.h player_state.h say_message_builder.h see_state.h self_object.h soccer_action.h soccer_intention.h view_area.h view_grid_map.h view_mode.h visual_sensor.h world_model.h '/ucrt64/include/rcsc/player'
make[3]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/player'
make[2]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/player'
Making install in coach
make[2]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/coach'
make[3]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/coach'
make[3]: Nothing to be done for 'install-exec-am'.
 /usr/bin/mkdir -p '/ucrt64/include/rcsc/coach'
 /usr/bin/install -c -m 644 coach_agent.h coach_audio_sensor.h coach_ball_object.h coach_command.h coach_config.h coach_debug_client.h coach_intercept_predictor.h coach_player_object.h coach_visual_sensor.h coach_world_model.h coach_world_state.h player_type_analyzer.h '/ucrt64/include/rcsc/coach'
make[3]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/coach'
make[2]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/coach'
Making install in trainer
make[2]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/trainer'
make[3]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc/trainer'
make[3]: Nothing to be done for 'install-exec-am'.
 /usr/bin/mkdir -p '/ucrt64/include/rcsc/trainer'
 /usr/bin/install -c -m 644 trainer_agent.h trainer_command.h trainer_config.h '/ucrt64/include/rcsc/trainer'
make[3]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/trainer'
make[2]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc/trainer'
Making install in .
make[2]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc'
make[3]: Entering directory '/d/CODING/RoboCup2D/librcsc/rcsc'
 /usr/bin/mkdir -p '/ucrt64/lib'
 /bin/sh ../libtool   --mode=install /usr/bin/install -c   librcsc.la '/ucrt64/lib'
libtool: install: /usr/bin/install -c .libs/librcsc.dll.a /ucrt64/lib/librcsc.dll.a
libtool: install: base_file=`basename librcsc.la`
libtool: install:  dlpath=`/bin/sh 2>&1 -c '. .libs/'librcsc.la'i; echo librcsc-19.dll'`
libtool: install:  dldir=/ucrt64/lib/`dirname ../bin/librcsc-19.dll`
libtool: install:  test -d /ucrt64/lib/../bin || mkdir -p /ucrt64/lib/../bin
libtool: install:  /usr/bin/install -c .libs/librcsc-19.dll /ucrt64/lib/../bin/librcsc-19.dll
libtool: install:  chmod a+x /ucrt64/lib/../bin/librcsc-19.dll
libtool: install:  if test -n '' && test -n 'strip --strip-unneeded'; then eval 'strip --strip-unneeded /ucrt64/lib/../bin/librcsc-19.dll' || exit 0; fi
libtool: install: /usr/bin/install -c .libs/librcsc.lai /ucrt64/lib/librcsc.la
 /usr/bin/mkdir -p '/ucrt64/include/rcsc'
 /usr/bin/install -c -m 644 types.h geom.h gz.h rcg.h factory.h game_mode.h game_time.h math_util.h random.h soccer_math.h timer.h version.h '/ucrt64/include/rcsc'
make[3]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc'
make[2]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc'
make[1]: Leaving directory '/d/CODING/RoboCup2D/librcsc/rcsc'
Making install in example
make[1]: Entering directory '/d/CODING/RoboCup2D/librcsc/example'
make[2]: Entering directory '/d/CODING/RoboCup2D/librcsc/example'
make[2]: Nothing to be done for 'install-exec-am'.
make[2]: Nothing to be done for 'install-data-am'.
make[2]: Leaving directory '/d/CODING/RoboCup2D/librcsc/example'
make[1]: Leaving directory '/d/CODING/RoboCup2D/librcsc/example'
Making install in src
make[1]: Entering directory '/d/CODING/RoboCup2D/librcsc/src'
make[2]: Entering directory '/d/CODING/RoboCup2D/librcsc/src'
 /usr/bin/mkdir -p '/ucrt64/bin'
  /bin/sh ../libtool   --mode=install /usr/bin/install -c rclmscheduler.exe rclmtableprinter.exe rcg2csv.exe rcg2txt.exe rcgrenameteam.exe rcgresultprinter.exe rcgreverse.exe rcgvalidator.exe rcgverconv.exe rcgversion.exe '/ucrt64/bin'
libtool: install: /usr/bin/install -c .libs/rclmscheduler.exe /ucrt64/bin/rclmscheduler.exe
libtool: install: /usr/bin/install -c .libs/rclmtableprinter.exe /ucrt64/bin/rclmtableprinter.exe
libtool: install: /usr/bin/install -c .libs/rcg2csv.exe /ucrt64/bin/rcg2csv.exe
libtool: install: /usr/bin/install -c .libs/rcg2txt.exe /ucrt64/bin/rcg2txt.exe
libtool: install: /usr/bin/install -c .libs/rcgrenameteam.exe /ucrt64/bin/rcgrenameteam.exe
libtool: install: /usr/bin/install -c .libs/rcgresultprinter.exe /ucrt64/bin/rcgresultprinter.exe
libtool: install: /usr/bin/install -c .libs/rcgreverse.exe /ucrt64/bin/rcgreverse.exe
libtool: install: /usr/bin/install -c .libs/rcgvalidator.exe /ucrt64/bin/rcgvalidator.exe
libtool: install: /usr/bin/install -c .libs/rcgverconv.exe /ucrt64/bin/rcgverconv.exe
libtool: install: /usr/bin/install -c .libs/rcgversion.exe /ucrt64/bin/rcgversion.exe
make[2]: Nothing to be done for 'install-data-am'.
make[2]: Leaving directory '/d/CODING/RoboCup2D/librcsc/src'
make[1]: Leaving directory '/d/CODING/RoboCup2D/librcsc/src'
make[1]: Entering directory '/d/CODING/RoboCup2D/librcsc'
make[2]: Entering directory '/d/CODING/RoboCup2D/librcsc'
 /usr/bin/mkdir -p '/ucrt64/bin'
 /usr/bin/install -c librcsc-config librcscenv '/ucrt64/bin'
 /usr/bin/mkdir -p '/ucrt64/lib/pkgconfig'
 /usr/bin/install -c -m 644 librcsc.pc '/ucrt64/lib/pkgconfig'
make[2]: Leaving directory '/d/CODING/RoboCup2D/librcsc'
make[1]: Leaving directory '/d/CODING/RoboCup2D/librcsc'
```

</details>

## librcsc 使用

下面是一个调用库的最小范例。
```cpp
#include <iostream>
#include <rcsc/version.h>

int main() {
    std::cout << "librcsc check ok" << std::endl;
    return 0;
}
```

你可以用下面的命令编译这个程序：
```sh
g++ -o test test.cpp $(pkg-config --cflags --libs librcsc)
```

或者写CMakeLists.txt：
```
cmake_minimum_required(VERSION 3.16)
project(librcsc_demo CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(PkgConfig REQUIRED)
pkg_check_modules(LIBRCSC REQUIRED librcsc)

add_executable(demo main.cpp)
target_include_directories(demo PRIVATE ${LIBRCSC_INCLUDE_DIRS})
target_link_directories(demo PRIVATE ${LIBRCSC_LIBRARY_DIRS})
target_link_libraries(demo PRIVATE ${LIBRCSC_LIBRARIES})
target_compile_options(demo PRIVATE ${LIBRCSC_CFLAGS_OTHER})
```

使用cmake的命令如下：
```sh
mkdir -p build
cd build
cmake -G "Unix Makefiles" ..
cmake --build .
./demo.exe
```