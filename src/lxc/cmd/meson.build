# SPDX-License-Identifier: LGPL-2.1-or-later

cmd_liblxc_includes = include_directories(
	'.',
	'../',
	'../cgroups',
	'../lsm',
	'../storage',
	'../../include',
	'../../../')

cmd_common_sources = files(
	'../af_unix.c',
	'../af_unix.h',
	'../attach_options.h',
	'../caps.c',
	'../caps.h',
	'../commands.c',
	'../commands.h',
	'../commands_utils.c',
	'../commands_utils.h',
	'../compiler.h',
	'../conf.c',
	'../conf.h',
	'../confile.c',
	'../confile.h',
	'../confile_utils.c',
	'../confile_utils.h',
	'../cgroups/cgfsng.c',
	'../cgroups/cgroup.c',
	'../cgroups/cgroup.h',
	'../cgroups/cgroup2_devices.c',
	'../cgroups/cgroup2_devices.h',
	'../cgroups/cgroup_utils.c',
	'../cgroups/cgroup_utils.h',
	'../error.c',
	'../error.h',
	'../initutils.c',
	'../initutils.h',
	'../file_utils.c',
	'../file_utils.h',
	'../lsm/apparmor.c',
	'../lsm/lsm.c',
	'../lsm/lsm.h',
	'../lsm/nop.c',
	'../lsm/selinux.c',
	'../lxcseccomp.h',
	'../lxclock.c',
	'../lxclock.h',
	'../macro.h',
	'../mainloop.c',
	'../mainloop.h',
	'../memory_utils.h',
	'../monitor.c',
	'../monitor.h',
	'../mount_utils.c',
	'../mount_utils.h',
	'../namespace.c',
	'../namespace.h',
	'../network.c',
	'../network.h',
	'../nl.c',
	'../nl.h',
	'../parse.c',
	'../parse.h',
	'../process_utils.c',
	'../process_utils.h',
	'../ringbuf.c',
	'../ringbuf.h',
	'../seccomp.c',
	'../start.c',
	'../start.h',
	'../state.c',
	'../state.h',
	'../storage/btrfs.c',
	'../storage/btrfs.h',
	'../storage/dir.c',
	'../storage/dir.h',
	'../storage/loop.c',
	'../storage/loop.h',
	'../storage/lvm.c',
	'../storage/lvm.h',
	'../storage/nbd.c',
	'../storage/nbd.h',
	'../storage/overlay.c',
	'../storage/overlay.h',
	'../storage/rbd.c',
	'../storage/rbd.h',
	'../storage/rsync.c',
	'../storage/rsync.h',
	'../storage/storage.c',
	'../storage/storage.h',
	'../storage/storage_utils.c',
	'../storage/storage_utils.h',
	'../storage/zfs.c',
	'../storage/zfs.h',
	'../string_utils.c',
	'../string_utils.h',
	'../sync.c',
	'../sync.h',
	'../terminal.c',
	'../terminal.h',
	'../utils.c',
	'../utils.h',
	'../uuid.c',
	'../uuid.h',
	'../log.h',
	'../log.c') + include_sources

cmd_lxc_init_sources = files(
	'lxc_init.c',
	'../af_unix.c',
	'../af_unix.h',
	'../caps.c',
	'../caps.h',
	'../error.c',
	'../error.h',
	'../file_utils.c',
	'../file_utils.h',
	'../initutils.c',
	'../initutils.h',
	'../log.h',
	'../log.c',
	'../macro.h',
	'../memory_utils.h',
	'../namespace.c',
	'../namespace.h',
	'../string_utils.c',
	'../string_utils.h') + include_sources

cmd_lxc_init_static_sources = files(
	'lxc_init.c',
	'../af_unix.c',
	'../af_unix.h',
	'../caps.c',
	'../caps.h',
	'../error.c',
	'../error.h',
	'../file_utils.c',
	'../file_utils.h',
	'../initutils.c',
	'../initutils.h',
	'../log.h',
	'../log.c',
	'../macro.h',
	'../memory_utils.h',
	'../namespace.c',
	'../namespace.h',
	'../string_utils.c',
	'../string_utils.h') + include_sources

cmd_lxc_monitord_sources = files('lxc_monitord.c') + cmd_common_sources + netns_ifaddrs_sources
cmd_lxc_user_nic_sources = files('lxc_user_nic.c') + cmd_common_sources + netns_ifaddrs_sources
cmd_lxc_usernsexec_sources = files('lxc_usernsexec.c') + cmd_common_sources + netns_ifaddrs_sources

cmd_lxc_checkconfig = configure_file(
			configuration : dummy_config_data,
                        input : 'lxc-checkconfig.in',
                        output : 'lxc-checkconfig')
install_data(join_paths(project_build_root, 'src/lxc/cmd/lxc-checkconfig'), install_dir : bindir)

cmd_lxc_update_config_data = configuration_data()
cmd_lxc_update_config = configure_file(
			configuration : dummy_config_data,
                        input : 'lxc-update-config.in',
                        output : 'lxc-update-config')
install_data(join_paths(project_build_root, 'src/lxc/cmd/lxc-update-config'), install_dir : bindir)

cmd_lxc_update_config_data = configuration_data()

cmd_programs += executable(
		'init.lxc.static',
		cmd_lxc_init_sources,
		include_directories: cmd_liblxc_includes,
		link_with : [liblxc_static],
		link_args : ['-static'],
		c_args : ['-DNO_LXC_CONF'],
		dependencies : [libcap_static],
		install : true)

cmd_programs += executable(
		'lxc-init',
		cmd_lxc_init_sources,
		include_directories: cmd_liblxc_includes,
		dependencies : liblxc_dep,
		install : true)

cmd_programs += executable(
		'lxc-monitord',
		cmd_lxc_monitord_sources,
		include_directories: cmd_liblxc_includes,
		dependencies : liblxc_dep,
		install : true)

cmd_programs += executable(
		'lxc-user-nic',
		cmd_lxc_user_nic_sources,
		include_directories: cmd_liblxc_includes,
		dependencies : liblxc_dep,
		install : true)

cmd_programs += executable(
		'lxc-usernsexec',
		cmd_lxc_usernsexec_sources,
		include_directories: cmd_liblxc_includes,
		dependencies : liblxc_dep,
		install : true)
