gnome = import('gnome')

gnome.compile_resources('aspinwall',
  join_paths('stylesheet', 'aspinwall.gresource.xml'),
  gresource_bundle: true,
  install: true,
  install_dir: pkgdatadir,
)

install_data('org.dithernet.aspinwall.launcher.gschema.xml',
  install_dir: join_paths(get_option('datadir'), 'glib-2.0/schemas')
)

install_data('org.dithernet.aspinwall.shell.gschema.xml',
  install_dir: join_paths(get_option('datadir'), 'glib-2.0/schemas')
)

compile_schemas = find_program('glib-compile-schemas', required: false)
if compile_schemas.found()
  test('Validate schema file', compile_schemas,
    args: ['--strict', '--dry-run', meson.current_source_dir()]
  )
endif

conf = configuration_data()
conf.set('VERSION', meson.project_version())
conf.set('pkgdatadir', pkgdatadir)

configure_file(
  input: 'start-aspinwall.in',
  output: 'start-aspinwall',
  configuration: conf,
  install: true,
  install_dir: get_option('bindir')
)

subdir('icons')
subdir('stylesheet')
subdir('x11')
