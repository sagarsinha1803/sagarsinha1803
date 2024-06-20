awk -v start="2024-06-20 10:05:00" '$0 ~ start, /^[0-9]{4}-[0-9]{2}-[0-9]{2} [0-9]{2}:[0-9]{2}:[0-9]{2}/ && NR>1 {print}' path_to_your_log_file.log



awk -v start="2024-06-20 10:05:00" '
    {
        if ($0 ~ /^[0-9]{4}-[0-9]{2}-[0-9]{2} [0-9]{2}:[0-9]{2}:[0-9]{2}/) {
            if ($0 >= start || capture == 1) {
                capture = 1
                print
            }
        } else if (capture == 1) {
            print
        }
    }
' path_to_your_log_file.log
