# Count post Blog time

Add below code to file `blog.js`

1.  Add data mont with array for get month name

    ```javascript
    const month = [
      'January',
      'February',
      'March',
      'April',
      'May',
      'June',
      'July',
      'August',
      'September',
      'October',
      'November',
      'December',
    ];
    ```

2.  Make function `getFullTime`

    ```javascript
    function getFullTime(time) {
      const date = time.getDate();
      const monthIndex = time.getMonth();
      const year = time.getFullYear();

      const hours = time.getHours();
      const minutes = time.getMinutes();

      return `${date} ${month[monthIndex]} ${year} ${hours}:${minutes} WIB`;
    }
    ```

3.  Make function `getDistanceTime`

    ```javascript
    function getDistanceTime(time) {
      const distance = new Date() - new Date(time);

      // Convert to day
      const miliseconds = 1000;
      const secondsInMinute = 3600; //Second in 1 minute
      const hoursInDay = 23;
      const dayDistance =
        distance / (miliseconds * secondsInMinute * hoursInDay);

      if (dayDistance >= 1) {
        return Math.floor(dayDistance) + ' day ago';
      } else {
        // Convert to hour
        const hourDistance = Math.floor(distance / (1000 * 60 * 60));
        if (hourDistance > 0) {
          return hourDistance + ' hour ago';
        } else {
          // Convert to minute
          const minuteDistance = Math.floor(distance / (1000 * 60));
          return minuteDistance + ' minute ago';
        }
      }
    }
    ```

4.  After create function `getDistanceTime` add this code to function `renderBlog` in

    Modify below code

    ```html
    ...
    <div class="detail-blog-content">
      ${getFullTime(blogs[i].postedAt)} | ${blogs[i].author}
    </div>
    <p>${blogs[i].content}</p>
    ...
    ```

    Add below code

    ```html
    ...
    <div style="text-align: right">
      <span style="font-size: 13px; color: grey">
        ${getDistanceTime(blogs[i].postedAt)}
      </span>
    </div>
    ...
    ```

5.  Call `renderBlog` function with `setInterval` function

    ```javascript
    ...
    setInterval(() => {
    console.log('render');
    renderBlog();
    }, 3000);
    ```
