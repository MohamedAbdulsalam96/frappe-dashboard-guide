# How To Guide: Frappe Form Dashboards

## Introduction

Frappe has hidden Form Dashboard features which can help make our forms a lot more user friendly. These features are not well-documented, so this guide aims to provide a comprehensive overview of how to use them effectively.

## Source
[Frappe's Form Dashboard code](https://github.com/frappe/frappe/blob/60df96ce0850d8952eb810070b5e8faf12e37aaa/frappe/public/js/frappe/form/dashboard.js)

## Features

The dashboard is part of the form and consists of several sections:

1. Progress Area
2. Heatmap Area
3. Chart Area
4. Stats Area
5. Connections Area (for related documents)
6. Custom Section Area
7. Headline Area
8. Badge Area

## Key Features and Implementation

### 1. Progress Indicators

Use progress indicators to show completion status or any quantitative measure.

```javascript
frm.dashboard.add_progress(title, percent, message) 
frm.dashboard.show_progress(title, percent, message) 
```

Usage:
```javascript
frm.dashboard.add_progress("Task Completion", 75, "3 of 4 tasks completed");
frm.dashboard.show_progress("Task Completion", 80, "4 of 5 tasks completed");
```

### 2. Heatmaps

Heatmaps are great for showing activity over time.

```javascript
frm.dashboard.render_heatmap()
```

Usage:
```javascript
frm.dashboard.render_heatmap({
    data: {
        dataPoints: {
            "1632441600": 5,
            "1632528000": 8,
            // ... more data points
        },
        start: new Date("2021-09-24"),
        end: new Date("2022-09-23")
    }
});
```

### 3. Charts and Graphs

Add visual representations of data with charts:

```javascript
render_graph(args) 
```

Usage:
```javascript
frm.dashboard.render_graph({
    data: {
        labels: ["Jan", "Feb", "Mar", "Apr", "May"],
        datasets: [{
            name: "Sales",
            values: [100, 120, 115, 110, 125]
        }]
    },
    type: 'line',
    colors: ['#7cd6fd']
});
```

### 4. Stat Indicators

Display key statistics or metrics:

```javascript
frm.dashboard.add_indicator(label, color)
```

Usage:
```javascript
frm.dashboard.add_indicator("Total Sales", "green");
frm.dashboard.add_indicator("Pending Orders", "orange");
```

### 5. Related Documents (Transactions)

Show links to related documents:

```javascript
frm.dashboard.add_transactions(opts)
```

Usage:
```javascript
frm.dashboard.add_transactions({
    label: "Related Documents",
    items: ["Sales Order", "Delivery Note", "Sales Invoice"]
});
```

### 6. Custom Sections

Add custom HTML sections to the dashboard:

```javascript
frm.dashboard.add_section(body_html, label = null, css_class = "custom", hidden = false)
```

Usage:
```javascript
let custom_section = frm.dashboard.add_section(
    `<h3>Custom Information</h3> <p>This is a custom section with any HTML content.</p>`,
    "My Custom Section"
);
```

### 7. Dynamic Updates

Update dashboard elements based on user actions or server responses:

```javascript
frm.dashboard.set_headline(html, color, permanent = false)

frm.dashboard.clear_headline()
```

Usage:
```javascript
frm.dashboard.set_headline("Document is under review", "orange");
frm.dashboard.clear_headline();
```

### 8. Badges and Counts

Display counts for related documents:

```javascript
frm.dashboard.set_badge_count_for_external_link(doctype, open_count, count)
```

Usage:
```javascript
frm.dashboard.set_badge_count_for_external_link("Sales Order", 5, 10);
```

### 9. Additional Dashboard Methods

There are several other useful methods:

#### Reset Dashboard

Reset the entire dashboard to its initial state:

```javascript
frm.dashboard.reset()
```

#### Hide and Show Dashboard

Control the visibility of the entire dashboard:

```javascript
frm.dashboard.hide()

frm.dashboard.show()
```

#### Clear Sections

Remove specific sections from the dashboard:

```javascript
frm.dashboard.clear_section(section_name)
```

Usage:
```javascript
frm.dashboard.clear_section("chart");
```

#### Set Document Status

Update the status indicator of the document:

```javascript
frm.dashboard.set_docstatus_icon(status)
```

Usage:
```javascript
frm.dashboard.set_docstatus_icon("Submitted");
``` 

#### Add Comments

Add a comment section to the form:

```javascript
frm.dashboard.add_comment(text, alert_class, permanent) 
```

Usage:
```javascript
frm.dashboard.add_comment("New comment added", "alert-info", false);
```

### Conclusion
This guide provides an overview of the key features available in Frappe's Form Dashboard. We can use these functions to create more informative and interactive form experiences for our users. Remember to refer to the [source code](https://github.com/frappe/frappe/blob/60df96ce0850d8952eb810070b5e8faf12e37aaa/frappe/public/js/frappe/form/dashboard.js) for the most up-to-date implementation details and additional features.

Please share screenshots and your usage examples on [Frappe Forum](), and make pull requests to make improvements.
