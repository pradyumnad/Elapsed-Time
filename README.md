Elapsed-Time
============

Used to get the elapsed time in string format from NSDate.

    /*
     *  params      :   date (NSDate)
     *  returns     :   elapsed Value (NSString)
     */

    - (NSString *)elapsedTimeSince:(NSDate *)date {
        NSTimeInterval timeInterval = [date timeIntervalSinceNow];
        NSAssert(timeInterval<0, @"Please provide past date for elapsed time");
    
        timeInterval = abs(timeInterval);
    
        double seconds = 60;
        double minutes = 60;
        double hours = 24;
    
        int noOfSeconds = fmod(timeInterval, seconds);
        int noOfMinutes = timeInterval/seconds;
    
        if (noOfMinutes == 0) {
            return [NSString stringWithFormat:@"%d seconds ago", (int)noOfSeconds];
        } else if (noOfMinutes > 0) {
            int noOfHours = noOfMinutes/minutes;
            if (noOfHours == 0) {
                return [NSString stringWithFormat:@"%d %@ ago", (int)noOfMinutes, (int)noOfMinutes == 1? @"Minute":@"Minutes"];
            } else {
                int noOfDays = noOfHours/hours;
                if (noOfDays == 0) {
                    return [NSString stringWithFormat:@"%d %@ ago", (int)noOfHours, (int)noOfHours == 1? @"Hour":@"Hours"];
                } else {
                    NSDateFormatter *dateFormatter = [[NSDateFormatter alloc] init];
                    [dateFormatter setDateFormat:@"MMM d, y"];
                    return [dateFormatter stringFromDate:date];
                }
            }
        }
        return @"";
    }