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




awk -v start="2024-06-20 10:05:00" '
    {
        if ($0 ~ /^[0-9]{4}-[0-9]{2}-[0-9]{2} [0-9]{2}:[0-9]{2}:[0-9]{2}/) {
            datetime = $0
            sub(/\..*/, "", datetime) # Remove milliseconds if present
            if (datetime >= start || capture == 1) {
                capture = 1
                print
            }
        } else if (capture == 1) {
            print
        }
    }
' path_to_your_log_file.log




awk -v end="$(date -d '1 hour ago' '+%Y-%m-%d %H:%M:%S')" '
    {
        timestamp = substr($0, 1, 19);  # Extract datetime part assuming it's in the first 19 characters
        if (timestamp >= end) {
            print
        }
    }
' path_to_your_log_file.log
