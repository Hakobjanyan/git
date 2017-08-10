 public String getEndOfTimer(){
        long duration = 0;
        Integer howMuchTimePassed = (Integer) dataObjectController.getInstance().getFields().get("howMuchTimePassed").getValue(); // 300
        StringBuilder result = new StringBuilder();
        if (howMuchTimePassed == null) howMuchTimePassed = 0;

        if (howMuchTimePassed==14400){
            result.append("- 03:00:00");
        }else {
            String s = elUtils.prettyDuration(new Long(howMuchTimePassed * 1000));
            int hours = 0, minutes = 0, seconds = 0;
            if (s.contains("ч")) {
                hours = Integer.parseInt(s.substring(1, s.indexOf("ч")));
            }
            if (s.contains("м")) {
                if (hours > 0) {
                    minutes = Integer.parseInt(s.substring(s.indexOf("ч") + 2, s.indexOf("м")));
                } else {
                    minutes = Integer.parseInt(s.substring(2, s.indexOf("м")));
                }
            }
            if (s.contains("с")) {
                if (minutes > 0) {
                    seconds = Integer.parseInt(s.substring(s.indexOf("м") + 2, s.length() - 1));
                } else {
                    seconds = Integer.parseInt(s.substring(3, s.length() - 1));
                }
            }


            /*******************Format #1*******************/
            if (hours < 1) {
                result.append("00:");
                if (59 - minutes < 10) {
                    result.append("0" + String.valueOf(59 - minutes));
                } else {
                    result.append(String.valueOf((59 - minutes)));
                }
                result.append(":");

                if (59 - seconds < 10) {
                    result.append("0" + String.valueOf(59 - seconds));
                } else {
                    result.append(String.valueOf((59 - seconds)));
                }
            }

            /*******************Format #2*******************/
            if (hours > 1 || hours == 1) {
                result.append("- ");
                result.append("0" + String.valueOf(hours - 1));
                result.append(":");
                if (minutes < 10) {
                    result.append("0" + String.valueOf(minutes));
                } else {
                    result.append(String.valueOf(minutes));
                }
                result.append(":");
                if (seconds < 10) {
                    result.append("0" + String.valueOf(seconds));
                } else {
                    result.append(String.valueOf(seconds));
                }
            }

            /*******************Format #3*******************/
            //if (hours > 2) result.append("- 03:00:00");
        }
        return result.toString();
    }