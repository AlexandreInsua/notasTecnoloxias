htop - ferramenta para visualizar procesos
  `htop`


Borrar directorio recurrentemente
  `rm -fr directorio`

Buscar os directorios de node_modules
  `find . -name "node_modules" -type d -prune | xargs du -chs`

Eliminar os directoros de node_modules
  `find . -name 'node_modules' -type d -prune -print -exec rm -rf '{}' \;`
