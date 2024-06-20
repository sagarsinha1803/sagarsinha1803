awk -v start="2024-06-20 10:05:00" '$0 ~ start, /^[0-9]{4}-[0-9]{2}-[0-9]{2} [0-9]{2}:[0-9]{2}:[0-9]{2}/ && NR>1 {print}' path_to_your_log_file.log
