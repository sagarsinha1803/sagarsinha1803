awk '
/^\d{4}-\d{2}-\d{2} \d{2}:\d{2}:\d{2},\d{3}/ { 
    if (entry) { 
        entries[++count] = entry;
        entry = "";
    } 
}
{
    entry = entry $0 "\n";
}
END { 
    if (entry) entries[++count] = entry;
    for (i = count-9; i <= count; i++) {
        if (i > 0) print entries[i];
    }
}
' logfile.log
