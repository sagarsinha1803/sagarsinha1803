awk '
/^\d{4}-\d{2}-\d{2} \d{2}:\d{2}:\d{2},\d{3}/ {
    if (entry) {
        entries[count % 10] = entry;
        count++;
        entry = "";
    }
}
{
    entry = entry $0 "\n";
}
END {
    if (entry) {
        entries[count % 10] = entry;
        count++;
    }
    start = (count > 10) ? count - 10 : 0;
    for (i = start; i < count; i++) {
        printf "%s", entries[i % 10];
    }
}
' logfile.log
