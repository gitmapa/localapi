## Restore dump

Para restaurar los .dump, correr desde bash

´´´
pg_restore \
  -U postgres \
  -h localhost \
  -p 5432 \
  -d ranie_app \
  --clean \
  --if-exists \
  --no-owner \
  --no-privileges \
  -v "/c/temp/ranie.dump" 
  ´´´