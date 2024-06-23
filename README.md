awk -v last_hour=$(date -d '1 hour ago' '+%Y-%m-%d %H:%M:%S') '
BEGIN { gsub(/[-:]/, "", last_hour); }
/^\d{4}-\d{2}-\d{2} \d{2}:\d{2}:\d{2},\d{3}/ {
  datetime = substr($1, 1, 10) substr($2, 1, 8);
  gsub(/[-:]/, "", datetime);
  if (datetime >= last_hour) printing = 1;
  else printing = 0;
}
{
  if (printing) print;
}
' logfile.log
