
[Mertics](#performance-metrics-parameters)

[Quick start](#quick-start)


**Note :** this is not a complete api. some methods are missing , only for refference

```js
Web Performance API
│
├── Performance Interface
│   ├── now() -> DOMHighResTimeStamp: Returns the current high-res timestamp
│   ├── timeOrigin -> DOMHighResTimeStamp: Time when navigation started
│   ├── eventCounts -> PerformanceEventCounts: Tracks input event counts (NEW)
│   ├── measureUserAgentSpecificMemory() -> Promise<MemoryMeasurement>: Measures memory use (NEW)
│   ├── clearMarks([name]) -> void: Clears named or all marks
│   ├── clearMeasures([name]) -> void: Clears named or all measures
│   ├── setResourceTimingBufferSize(size: unsigned long) -> void: Sets buffer size for resource timing entries
│   ├── getEntriesByType(type: string) -> PerformanceEntry[]: Fetches entries of a specific type (e.g., 'mark', 'measure')
│   ├── getEntriesByName(name: string) -> PerformanceEntry[]: Fetches entries by name
│   ├── toJSON() -> object: Returns JSON serialization
│   └── onresourcetimingbufferfull -> event handler: Triggered when resource timing buffer is full
│
├── Performance Timeline API
│   ├── PerformanceEntry Interface
│   │   ├── name -> string: Entry name
│   │   ├── entryType -> string: Type of performance entry (e.g., 'resource', 'mark')
│   │   ├── startTime -> double: Start time of the entry
│   │   ├── duration -> double: Duration of the entry
│   │   └── toJSON() -> object: JSON serialization of entry
│   ├── getEntries() -> PerformanceEntry[]: Fetches all performance entries
│   ├── getEntriesByName(name: string, type?: string) -> PerformanceEntry[]: Entries by name and optionally by type
│   └── getEntriesByType(type: string) -> PerformanceEntry[]: Entries by type
│
├── Navigation Timing API
│   ├── PerformanceNavigationTiming Interface (extends PerformanceEntry)
│   │   ├── unloadEventStart -> double: Unload event start timestamp
│   │   ├── unloadEventEnd -> double: Unload event end timestamp
│   │   ├── domContentLoadedEventStart -> double: DOMContentLoaded event start
│   │   ├── domContentLoadedEventEnd -> double: DOMContentLoaded event end
│   │   ├── redirectCount -> unsigned long: Number of redirects
│   │   ├── type -> string: Type of navigation ('navigate', 'reload', etc.)
│   │   ├── domInteractive -> double: Time DOM became interactive
│   │   ├── loadEventStart -> double: Start of the load event
│   │   ├── loadEventEnd -> double: End of the load event
│   │   ├── responseStart -> double: Start of response from the server
│   │   ├── responseEnd -> double: End of response from the server
│   │   └── toJSON() -> object: JSON serialization
│
├── Resource Timing API
│   ├── PerformanceResourceTiming Interface (extends PerformanceEntry)
│   │   ├── initiatorType -> string: Type of resource (e.g., 'script', 'img')
│   │   ├── fetchStart -> double: Start time of fetch operation
│   │   ├── domainLookupStart -> double: DNS lookup start
│   │   ├── domainLookupEnd -> double: DNS lookup end
│   │   ├── connectStart -> double: Connection start time
│   │   ├── connectEnd -> double: Connection end time
│   │   ├── secureConnectionStart -> double: Start of the TLS handshake
│   │   ├── requestStart -> double: Start of the request
│   │   ├── responseStart -> double: Start of receiving the response
│   │   ├── responseEnd -> double: End of receiving the response
│   │   ├── transferSize -> unsigned long: Size of the transferred resource
│   │   ├── encodedBodySize -> unsigned long: Encoded size of the body
│   │   ├── decodedBodySize -> unsigned long: Decoded size of the body
│   │   └── toJSON() -> object: JSON serialization of the resource timing
│   ├── clearResourceTimings() -> void: Clears all resource timings
│   ├── setResourceTimingBufferSize() -> void: Set resource timing buffer size
│   └── onresourcetimingbufferfull -> event handler: Triggered when buffer is full
│
├── User Timing API
│   ├── PerformanceMark Interface (extends PerformanceEntry)
│   │   ├── detail -> any: Optional data associated with the mark
│   │   └── toJSON() -> object: JSON serialization of the mark
│   ├── PerformanceMeasure Interface (extends PerformanceEntry)
│   │   ├── detail -> any: Optional data associated with the measure
│   │   └── toJSON() -> object: JSON serialization of the measure
│   ├── mark(name: string, options?: object) -> PerformanceMark: Records a mark
│   └── measure(name: string, startMark?: string, endMark?: string) -> PerformanceMeasure: Measures time between marks or timestamps
│
├── Paint Timing API
│   ├── PerformancePaintTiming Interface (extends PerformanceEntry)
│   │   ├── name -> string: 'first-paint' or 'first-contentful-paint'
│   │   ├── startTime -> double: Timestamp for paint event
│   │   └── toJSON() -> object: JSON serialization of paint timing entry
│   ├── First Paint -> double: Time of first paint
│   ├── First Contentful Paint -> double: Time of first contentful paint
│
├── Server Timing API
│   ├── PerformanceServerTiming Interface (extends PerformanceEntry)
│   │   ├── name -> string: Server timing metric name
│   │   ├── description -> string: Server timing metric description
│   │   ├── duration -> double: Server metric duration
│   │   └── toJSON() -> object: JSON serialization of server timing
│   └── getEntriesByType('server') -> PerformanceServerTiming[]: Returns server timing entries
│
├── Frame Timing API (Experimental)
│   ├── PerformanceFrameTiming Interface (extends PerformanceEntry)
│   │   ├── startTime -> double: Timestamp when the frame started
│   │   ├── duration -> double: Duration of the frame
│   │   └── toJSON() -> object: JSON serialization of frame timing
│
├── Long Tasks API
│   ├── PerformanceLongTaskTiming Interface (extends PerformanceEntry)
│   │   ├── name -> string: Name of the long task
│   │   ├── attribution -> PerformanceAttributionTiming[]: Contributors to the long task
│   │   ├── startTime -> double: Time when the long task started
│   │   ├── duration -> double: Duration of the long task
│   │   └── toJSON() -> object: JSON serialization of long task entry
│
├── Network Information API
│   ├── connection -> NetworkInformation: Provides network connection info
│   │   ├── downlink -> double: Effective bandwidth in Mbps
│   │   ├── effectiveType -> string: Effective connection type ('4g', '3g', etc.)
│   │   ├── rtt -> double: Round-trip time estimate in milliseconds
│   │   ├── saveData -> boolean: Whether user requested reduced data usage
│   └── onchange -> EventHandler: Fired when the network information changes
│
├── Memory API
│   ├── memory -> object: Provides memory usage information
│   │   ├── totalJSHeapSize -> double: Total allocated heap memory
│   │   ├── usedJSHeapSize -> double: Current memory being used
│   │   └── jsHeapSizeLimit -> double: Maximum heap size limit
│
├── Event Timing API (Experimental)
│   ├── PerformanceEventTiming Interface (extends PerformanceEntry)
│   │   ├── duration -> double: Duration of the event
│   │   ├── name -> string: Name of the event type (e.g., 'click', 'keydown')
│   │   ├── processingStart -> double: Time when event started processing
│   │   ├── processingEnd -> double: Time when event processing finished
│   │   └── toJSON() -> object: JSON serialization of the event timing
│
└── PerformanceObserver API
    ├── PerformanceObserver Interface
    │   ├── observe(options: object) -> void: Observes entries of given types
    │   ├── disconnect() -> void: Stops the observer
    │   └── takeRecords() -> PerformanceEntry[]: Retrieves performance records
    ├── PerformanceObserverEntryList Interface
    │   ├── getEntries() -> PerformanceEntry[]: Returns all performance entries
    │   ├── getEntriesByName(name: string) -> PerformanceEntry[]: Entries by name
    │   └── getEntriesByType(type: string) -> PerformanceEntry[]: Entries by type

```


<br>





## performance metrics parameters

Here’s a comprehensive list of **performance metrics parameters** that can be measured using the **Performance Timing API**, **Resource Timing API**, and other browser-based performance APIs. These can be leveraged in your Chrome extension to analyze different aspects of a webpage's performance:

### 1. **Navigation Timing API (performance.timing)**
Provides detailed timing information about the navigation process of a webpage:

- `navigationStart`: The time when the page navigation started.
- `unloadEventStart`: The time the unload event of the previous page started.
- `unloadEventEnd`: The time the unload event of the previous page finished.
- `redirectStart`: The time when the first HTTP redirect request started.
- `redirectEnd`: The time when the last HTTP redirect request completed.
- `fetchStart`: The time when the browser started to fetch the resource.
- `domainLookupStart`: The time when DNS lookup started.
- `domainLookupEnd`: The time when DNS lookup ended.
- `connectStart`: The time when the browser started to connect to the server.
- `connectEnd`: The time when the connection to the server completed.
- `secureConnectionStart`: The time when the SSL handshake process started.
- `requestStart`: The time when the browser sent the request to the server.
- `responseStart`: The time when the first byte of the response was received.
- `responseEnd`: The time when the full response was received.
- `domLoading`: The time when the browser started loading the DOM.
- `domInteractive`: The time when the browser finished parsing the HTML and DOM is ready.
- `domContentLoadedEventStart`: The time when the `DOMContentLoaded` event started.
- `domContentLoadedEventEnd`: The time when the `DOMContentLoaded` event ended.
- `domComplete`: The time when the DOM loading is complete.
- `loadEventStart`: The time when the load event started.
- `loadEventEnd`: The time when the load event ended.

### 2. **Resource Timing API (performance.getEntriesByType('resource'))**
Provides detailed timing information about resource loading:

- `startTime`: The time when the resource request was initiated.
- `redirectStart` / `redirectEnd`: Time for HTTP redirects.
- `domainLookupStart` / `domainLookupEnd`: Time spent in DNS lookup.
- `connectStart` / `connectEnd`: Time spent in establishing TCP connection.
- `secureConnectionStart`: Time spent in establishing a secure connection (HTTPS).
- `requestStart`: Time when the browser started sending the request.
- `responseStart`: Time when the first byte of the resource was received.
- `responseEnd`: Time when the full resource was received.
- `transferSize`: Total size of the resource transfer in bytes.
- `encodedBodySize`: The size of the resource after it was compressed.
- `decodedBodySize`: The size of the resource after it was decompressed.

### 3. **Paint Timing API (performance.getEntriesByType('paint'))**
Provides information about the timing of rendering key points on the page:

- `first-paint`: The time when the browser first rendered anything.
- `first-contentful-paint`: The time when the browser rendered the first bit of content (text, image, etc.).

### 4. **Long Tasks API (performance.getEntriesByType('longtask'))**
Provides information about tasks that run on the main thread for longer than 50ms:

- `startTime`: The time when the long task started.
- `duration`: How long the task took.
- `attribution`: Provides details about which script caused the long task.

### 5. **User Timing API (performance.mark and performance.measure)**
Allows you to define custom marks and measures in your code:

- `performance.mark()`: Marks a specific moment in time during the page load.
- `performance.measure()`: Measures the time between two marks.

### 6. **Memory API (performance.memory)**
Provides information about JavaScript heap memory usage:

- `totalJSHeapSize`: Total size of the allocated JavaScript heap.
- `usedJSHeapSize`: The amount of JavaScript heap currently being used.
- `jsHeapSizeLimit`: The maximum size the JavaScript heap is allowed to grow to.

### 7. **Network Information API**
Provides information about the network connection:

- `effectiveType`: The connection type (e.g., 4g, 3g, slow-2g).
- `downlink`: Estimated effective download bandwidth in Mbps.
- `rtt`: Round-trip time in milliseconds.
- `saveData`: Whether the user has requested a reduced data usage mode.

### 8. **Navigation Timing Level 2 API (performance.getEntriesByType('navigation'))**
Provides a more detailed breakdown of the page load process:

- `type`: The type of navigation (e.g., `reload`, `navigate`, `back_forward`).
- `redirectCount`: The number of redirects that occurred during navigation.

### 9. **Largest Contentful Paint (LCP)**
Measures the time it takes for the largest visible content element to load.

- `performance.getEntriesByType('largest-contentful-paint')`
- `startTime`: The time when the largest content element was painted.

### 10. **First Input Delay (FID)**
Measures the delay between the first user interaction (click, tap, etc.) and the time the browser responds to that interaction.

- Use the **First Input Delay API**: `performance.getEntriesByType('first-input')`

### 11. **Cumulative Layout Shift (CLS)**
Measures the visual stability of a webpage by tracking layout shifts.

- Use the **Layout Instability API**: `performance.getEntriesByType('layout-shift')`
  - `value`: The amount of layout shift that occurred.
  - `hadRecentInput`: Whether the shift happened after a user interaction.

### 12. **Time to First Byte (TTFB)**
Measures the time it takes for the server to send the first byte of the response.

- `performance.timing.responseStart - performance.timing.navigationStart`

### 13. **Time to Interactive (TTI)**
Measures the time until the page becomes fully interactive.

- Can be derived from **First Contentful Paint**, **First Input Delay**, and **Total Blocking Time** metrics.

### 14. **Total Blocking Time (TBT)**
Measures the total time during which the main thread was blocked and unable to respond to user input.

- Derived from the **Long Tasks API**: Sum of all task durations over 50ms.

### 15. **Service Worker API**
Provides information on service workers that control the page:

- `controller`: Indicates if the page is currently controlled by a service worker.

### 16. **Server Timing API**
Allows servers to pass back timing information:

- `performance.getEntriesByType('server')`: Timing data sent by the server (e.g., processing time).

---

### Example of Using Multiple Metrics
You can combine these metrics for a more comprehensive performance analysis:

```javascript
function analyzePerformance() {
    const timing = window.performance.timing;
    const fcp = performance.getEntriesByName("first-contentful-paint")[0]?.startTime || 0;
    const cls = performance.getEntriesByType('layout-shift').reduce((acc, shift) => acc + (shift.hadRecentInput ? 0 : shift.value), 0);
    const ttfb = timing.responseStart - timing.navigationStart;

    return {
        ttfb,
        fcp,
        cls,
        domContentLoaded: timing.domContentLoadedEventEnd - timing.navigationStart,
        totalLoadTime: timing.loadEventEnd - timing.navigationStart,
        firstInputDelay: performance.getEntriesByType('first-input')[0]?.processingStart - performance.getEntriesByType('first-input')[0]?.startTime || 0
    };
}
```

### Key Metrics for Performance Analysis:
- **Load Time**: `timing.loadEventEnd - timing.navigationStart`
- **First Contentful Paint (FCP)**: Time until the first piece of content is displayed.
- **Time to Interactive (TTI)**: Time until the page becomes fully interactive.
- **Cumulative Layout Shift (CLS)**: Measures layout shifts affecting user experience.
- **Total Blocking Time (TBT)**: Time the main thread was blocked by long tasks.
- **First Input Delay (FID)**: Delay between user interaction and browser response.

By using these metrics, you can build a detailed **Page Performance Analyzer** extension that helps developers optimize their pages in various ways.









## Quick Start


<br>

To effectively use the **Web Performance API** in development, it's important to understand where to start, key entry points, and how to refer to specific APIs during the development process. Below are detailed notes to guide you through the various entry points and ways to approach the API.

### 1. **Understanding the Web Performance API**
The **Web Performance API** provides developers with ways to measure and analyze performance metrics of web applications. These metrics help identify bottlenecks and optimize user experiences.

### 2. **Where to Start**
Before diving into specific APIs, it’s essential to start by:
- **Defining what you want to measure**: Page load time, resource fetch times, long task durations, etc.
- **Deciding on the type of performance** you need to track: 
  - **Navigation Timing** for page loads
  - **Resource Timing** for assets like images and scripts
  - **User Timing** for custom marks and measures
  - **Long Tasks API** to detect long-running tasks that block the main thread

Once you've identified your goals, you can decide which API suits your needs.

### 3. **Key Entry Points for the Web Performance API**
Here are the most common entry points that allow you to begin measuring web performance:

#### **1. `window.performance`**
The `performance` object is your main entry point. It provides methods and properties to collect performance-related data. You can access this object directly from the global `window` object.

**Example:**
```javascript
// Accessing the performance object
const performanceData = window.performance;

// Get the current time in milliseconds
const currentTime = performanceData.now();
console.log(currentTime);  // High-resolution time since page load
```

**Key Use-Cases:**
- **For all performance metrics**, use `window.performance`.
- **For custom metrics** (marks and measures), use `performance.mark()` and `performance.measure()`.

#### **2. `Performance.now()`**
This method returns a high-resolution timestamp representing the number of milliseconds elapsed since the page started loading. It’s the preferred method to track time with more precision than `Date.now()`.

**Example:**
```javascript
const start = performance.now();

// Code you want to measure
for (let i = 0; i < 1000000; i++) {
  // Some operation
}

const end = performance.now();
console.log(`Execution time: ${end - start} milliseconds`);
```

**Use-Case:**
- **For measuring durations of synchronous code**, like loops, user interactions, or function calls.

#### **3. `Performance.mark()` and `Performance.measure()`**
These methods allow you to define custom "marks" and "measures" to analyze specific sections of your code. Marks represent points in time, and measures represent the time difference between two marks.

**Example:**
```javascript
// Start a mark
performance.mark('startTask');

// Simulating some task
setTimeout(() => {
  performance.mark('endTask');

  // Measure time between startTask and endTask
  performance.measure('Task duration', 'startTask', 'endTask');

  const measures = performance.getEntriesByType('measure');
  console.log(measures);
}, 1000);
```

**Use-Case:**
- **For measuring specific code sections**, like user interactions, external API calls, or animations.

#### **4. `Performance.getEntriesByType()` and `Performance.getEntriesByName()`**
These methods allow you to retrieve performance entries for analysis. Depending on your goal, you can filter by type (e.g., 'resource', 'mark', 'measure') or by a specific name.

**Example:**
```javascript
// Fetch all resource entries (e.g., images, scripts)
const resourceEntries = performance.getEntriesByType('resource');
console.log(resourceEntries);

// Fetch all marks with a specific name
const markEntries = performance.getEntriesByName('startTask');
console.log(markEntries);
```

**Use-Case:**
- **For retrieving performance entries** to analyze how resources are loaded or custom marks/measures you’ve created.

### 4. **Specialized APIs Based on Use-Cases**

#### **1. Navigation Timing API**
If you want to measure how long it takes for the page to fully load, from the user clicking the link to the page being rendered, the **Navigation Timing API** gives you detailed information.

**Example:**
```javascript
const navigationData = performance.getEntriesByType('navigation')[0];
console.log(`Page load time: ${navigationData.loadEventEnd - navigationData.startTime} ms`);
```

**Use-Case:**
- **For measuring page load time**, redirects, and detailed timings from start to finish of a navigation event.

#### **2. Resource Timing API**
If you want to know how long individual resources (images, scripts, stylesheets) take to load, use the **Resource Timing API**.

**Example:**
```javascript
const resources = performance.getEntriesByType('resource');
resources.forEach(resource => {
  console.log(`${resource.name}: ${resource.duration} ms`);
});
```

**Use-Case:**
- **For optimizing assets**, like images, JavaScript, and CSS files. Identify which resources are slow.

#### **3. Paint Timing API**
If your goal is to measure **First Paint (FP)** or **First Contentful Paint (FCP)** to improve user-perceived performance, the **Paint Timing API** provides these metrics.

**Example:**
```javascript
const paintMetrics = performance.getEntriesByType('paint');
paintMetrics.forEach(metric => {
  console.log(`${metric.name}: ${metric.startTime} ms`);
});
```

**Use-Case:**
- **For improving perceived performance**, especially for measuring how soon something appears on the screen.

#### **4. Long Tasks API**
This API is useful for identifying tasks that take too long on the main thread, causing delays in rendering and interaction. Long tasks are often related to complex JavaScript operations that block user interactions.

**Example:**
```javascript
const observer = new PerformanceObserver((list) => {
  const entries = list.getEntries();
  entries.forEach(entry => {
    console.log(`Long task detected: ${entry.duration} ms`);
  });
});

observer.observe({ type: 'longtask', buffered: true });
```

**Use-Case:**
- **For identifying and debugging performance bottlenecks** caused by long tasks on the main thread.

### 5. **PerformanceObserver API**
This is a powerful tool that allows you to observe performance metrics in real time, particularly useful when you want to continuously monitor performance entries as they occur.

**Example:**
```javascript
const observer = new PerformanceObserver((list) => {
  const entries = list.getEntries();
  entries.forEach(entry => {
    console.log(`${entry.entryType}: ${entry.startTime} ms`);
  });
});

observer.observe({ entryTypes: ['navigation', 'resource', 'longtask', 'mark', 'measure'] });
```

**Use-Case:**
- **For continuous monitoring** of performance entries in real-time, particularly useful in single-page applications (SPAs).

### 6. **Referencing the Web Performance API**
While developing, it’s important to refer to the official **MDN Web Docs** or **W3C Performance Timeline Specification** for the most accurate and up-to-date information. Some pointers:
- **MDN Web Docs**: https://developer.mozilla.org/en-US/docs/Web/API/Performance
- **Chrome DevTools**: Chrome’s built-in tools help visualize performance metrics.
- **W3C Specification**: https://www.w3.org/TR/performance-timeline/

### 7. **Common Development Patterns**
- **Measuring load performance**: Use **Navigation Timing** or **Resource Timing** to get exact load times.
- **Custom performance marks**: Use **User Timing** with `performance.mark()` and `performance.measure()` to track specific code paths.
- **Real-time tracking**: Use **PerformanceObserver** for real-time, continuous tracking of metrics.
- **Visualizing data**: Use DevTools and visualization libraries (like **Perfume.js**) to visualize and log performance data.

### 8. **Tools for Performance Profiling**
You can integrate your code with performance tools like:
- **Lighthouse**: A web app auditing tool that integrates with Chrome DevTools to provide insights into performance, accessibility, SEO, and more.
- **WebPageTest**: An online tool to test web page performance and provide detailed breakdowns of load times and bottlenecks.

### Conclusion:
By knowing the right entry points and APIs, you can gather and analyze performance data, ultimately improving the performance and user experience of your web applications. Always keep performance optimization in mind throughout the development lifecycle, especially when managing resources, network requests, and complex JavaScript operations.








<br>


Here are **detailed notes** on the **entry points** to start using the **Web Performance API** and their various methods. These notes will help you understand the key access points, their roles, and how you can utilize them in different performance measurement scenarios:

### 1. **`window.performance`**
This is the main entry point for interacting with the Web Performance API. The `performance` object holds the entire set of methods and properties that provide access to performance metrics.

#### **Key Methods and Properties of `window.performance`:**

#### 1.1 **`performance.now()`**
- **Purpose**: Returns a high-resolution timestamp (in milliseconds) representing the time since the page started loading. This value has much higher precision than `Date.now()`.
- **Typical Use-Cases**:
  - Used to measure precise durations of events or operations in the web app.
  - Especially useful for timing synchronous code execution.

**Example:**
```javascript
const startTime = performance.now();

// Some code to measure
for (let i = 0; i < 1000000; i++) {
  // Intense operation
}

const endTime = performance.now();
console.log(`Execution took: ${endTime - startTime} ms`);
```

#### 1.2 **`performance.mark()`**
- **Purpose**: Creates a timestamp with a given name (a "mark") at the point in time when the method is called.
- **Typical Use-Cases**:
  - Useful for marking specific points in your code to measure the duration between them using `performance.measure()`.
  - Helpful in tracking user interaction points, like the start of a button click or an animation.

**Example:**
```javascript
performance.mark('startMark');
// Code you want to measure
performance.mark('endMark');
```

#### 1.3 **`performance.measure()`**
- **Purpose**: Measures the duration between two marks and records the result in the browser’s performance timeline. This is used in combination with `performance.mark()`.
- **Typical Use-Cases**:
  - Measure the performance between two named marks (like a start and end of an operation) or between the start of the page and the current point.
  - Helps in analyzing specific portions of code execution.

**Example:**
```javascript
performance.measure('measureTask', 'startMark', 'endMark');

const measures = performance.getEntriesByType('measure');
measures.forEach(measure => {
  console.log(`Duration of ${measure.name}: ${measure.duration} ms`);
});
```

#### 1.4 **`performance.getEntriesByType()`**
- **Purpose**: Returns an array of `PerformanceEntry` objects based on a specific type, such as 'navigation', 'resource', 'mark', 'measure', etc.
- **Typical Use-Cases**:
  - Retrieve entries for specific performance-related events like network requests (resource timing), custom marks, or page navigation timing.
  - Used to filter different types of performance entries and gather specific data for analysis.

**Example:**
```javascript
const resourceEntries = performance.getEntriesByType('resource');
resourceEntries.forEach(entry => {
  console.log(`${entry.name}: ${entry.duration} ms`);
});
```

#### 1.5 **`performance.getEntriesByName()`**
- **Purpose**: Retrieves performance entries by a specific name, which could be a custom mark or measure.
- **Typical Use-Cases**:
  - Filter out entries by their given name, typically used for custom marks or measures to pinpoint specific events.

**Example:**
```javascript
const entries = performance.getEntriesByName('startMark');
console.log(entries);  // Logs performance entries with the name 'startMark'
```

#### 1.6 **`performance.clearMarks()` and `performance.clearMeasures()`**
- **Purpose**: Clears any marks or measures that have been recorded in the browser's performance timeline. You can either clear a specific mark/measure by its name or clear all recorded marks/measures.
- **Typical Use-Cases**:
  - Clean up performance data after you've gathered and analyzed it.
  - Helpful when you have multiple runs of tests or timing points in a single page session and don’t want old data to accumulate.

**Example:**
```javascript
performance.clearMarks('startMark');
performance.clearMeasures('measureTask');
```

### 2. **`PerformanceObserver` API**
The **`PerformanceObserver` API** is used to observe performance entries in real-time as they are recorded by the browser. This is particularly useful when you want to dynamically observe certain types of performance events (e.g., resource load times, long tasks, custom marks) as they happen.

#### **Key Methods of `PerformanceObserver`:**

#### 2.1 **`PerformanceObserver.observe()`**
- **Purpose**: Starts the observation of specific types of performance entries (e.g., 'mark', 'measure', 'longtask', 'resource', etc.).
- **Typical Use-Cases**:
  - Use it when you need to track performance metrics continuously as new entries are logged (e.g., on user interactions or network activity).

**Example:**
```javascript
const observer = new PerformanceObserver((list) => {
  const entries = list.getEntries();
  entries.forEach(entry => {
    console.log(`${entry.entryType}: ${entry.startTime} ms, Duration: ${entry.duration} ms`);
  });
});

observer.observe({ entryTypes: ['mark', 'measure', 'resource', 'longtask'] });
```

#### 2.2 **`PerformanceObserver.disconnect()`**
- **Purpose**: Stops the observation of performance entries.
- **Typical Use-Cases**:
  - Use this to stop listening for performance events after gathering enough data, preventing resource waste in long-running applications.

**Example:**
```javascript
observer.disconnect();
```

### 3. **`PerformanceEntry` Interface**
When you retrieve performance data (through methods like `getEntries()`), each piece of data is represented by a **PerformanceEntry** object. This object contains properties that describe the entry, such as its name, type, start time, and duration.

#### **Key Properties of `PerformanceEntry`:**
- **`name`**: A string representing the name of the performance entry (e.g., the name of a resource or custom mark).
- **`entryType`**: The type of performance entry (e.g., 'mark', 'measure', 'resource', 'navigation').
- **`startTime`**: The timestamp when the performance event started.
- **`duration`**: The total time taken by the event, measured in milliseconds.

**Example:**
```javascript
const entry = performance.getEntriesByType('mark')[0];
console.log(`Name: ${entry.name}, Type: ${entry.entryType}, Start Time: ${entry.startTime}, Duration: ${entry.duration}`);
```

### 4. **Navigation Timing API**
If your goal is to analyze how long the page took to load or understand the individual stages of the page load process (DNS lookup, TCP connection, etc.), the **Navigation Timing API** provides a set of detailed metrics.

#### **Key Methods/Properties of Navigation Timing:**

#### 4.1 **`performance.timing`**
- **Purpose**: Provides detailed timing information related to the page navigation, from the start of the request to the final render.
- **Typical Use-Cases**:
  - Analyzing how long each phase of the page load took (e.g., DNS lookup time, DOMContentLoaded time, etc.).
  - Used for identifying performance bottlenecks in the loading of a web page.

**Example:**
```javascript
const timing = performance.timing;
console.log(`Time to DOMContentLoaded: ${timing.domContentLoadedEventEnd - timing.navigationStart} ms`);
```

### 5. **Resource Timing API**
This API provides timing information for fetching individual resources on the page, like images, scripts, stylesheets, etc. It's useful for optimizing resource loading and understanding which resources are slow.

#### **Key Methods/Properties of Resource Timing:**

#### 5.1 **`performance.getEntriesByType('resource')`**
- **Purpose**: Retrieves performance entries for individual resources, including start time, duration, and size.
- **Typical Use-Cases**:
  - Tracking resource load times (e.g., images, JavaScript files).
  - Identifying which resources are causing delays in page load.

**Example:**
```javascript
const resources = performance.getEntriesByType('resource');
resources.forEach(resource => {
  console.log(`Resource ${resource.name} took ${resource.duration} ms to load.`);
});
```

### 6. **Paint Timing API**
The **Paint Timing API** allows you to measure the time it takes to paint the first visual elements on the page. This can help in assessing how fast the user sees meaningful content.

#### **Key Methods/Properties of Paint Timing:**

#### 6.1 **`performance.getEntriesByType('paint')`**
- **Purpose**: Provides information about the first paint and first contentful paint events, which are crucial for user-perceived performance.
- **Typical Use-Cases**:
  - Measuring **First Paint (FP)** and **First Contentful Paint (FCP)**.
  - Use these metrics to optimize the speed of the initial content render on the page.

**Example:**
```javascript
const paintEntries = performance.getEntriesByType('paint');
paintEntries.forEach(entry => {
  console.log(`${entry.name}: ${entry.startTime} ms`);
});
```

### 7. **Long Tasks API**
The **Long Tasks API** helps detect long-running operations on the main thread that can block user interactions, such as long-running JavaScript execution or rendering tasks.

#### **Key Methods/Properties of Long Tasks:**

#### 7.1 **`Performance

Observer.observe({entryTypes: ['longtask']})`**
- **Purpose**: Observes long tasks in the main thread and collects information about tasks that took more than 50ms.
- **Typical Use-Cases**:
  - Use this API to identify and debug performance bottlenecks due to long tasks that negatively impact user experience.

**Example:**
```javascript
const observer = new PerformanceObserver((list) => {
  list.getEntries().forEach(entry => {
    console.log(`Long task detected: ${entry.duration} ms`);
  });
});

observer.observe({ entryTypes: ['longtask'] });
```

---
These are the core entry points and methods that you will use in the **Web Performance API** to measure and analyze performance on the web. Each method and property serves a specific purpose, allowing developers to gather precise metrics, optimize performance, and enhance user experiences.

