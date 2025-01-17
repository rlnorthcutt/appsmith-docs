---
description: >-
  In this part of the tutorial, you'll learn how to connect your app to a
  datasource and write a query.
---

# Connecting to Data Source

### **Connecting to Postgres Mock DB**

Appsmith supports various data sources and lets you write queries on them to perform different actions from the application. In this tutorial, you'll connect to a Postgres data source that has the following tables:

1. **Business Table**: It contains detailed information about a few businesses filtered from the Yelp Data.
2. **Review Table**: This table has reviews associated with the businesses listed in the business table.

{% hint style="info" %}
Appsmith supports various databases like:

* [Amazon S3 (also Upcloud, Digital Ocean Spaces, Wasabi, DreamObjects)](https://docs.appsmith.com/datasource-reference/querying-amazon-s3)
* [ArangoDB ](https://docs.appsmith.com/datasource-reference/querying-arango-db)
* [DynamoDB ](../../datasource-reference/querying-dynamodb.md)
* [ElasticSearch ](https://docs.appsmith.com/datasource-reference/querying-elasticsearch)
* [Firestore ](https://docs.appsmith.com/datasource-reference/querying-firestore)
* [MongoDB ](https://docs.appsmith.com/datasource-reference/querying-mongodb)
* [MySQL](https://docs.appsmith.com/datasource-reference/querying-mysql), and a [lot more](connecting-to-data-source-and-binding-queries.md#connecting-to-postgres-mock-db).
{% endhint %}

Let's utilize this mock data source to fetch all the business items for the Review Moderator app by following the below steps:

{% embed url="https://youtu.be/ZOSYloiB8ZY" %}
Connecting to a Datasource on Appsmith\

{% endembed %}

1. First, click on the `+` the icon next to the `Datasources`.
2. Next, you'll see a list of data source options that you can connect to.
3. Choose **Postgres** and rename the data source to `Postgres Mock DB`.
4. Next, use the following details to connect with the data source.

```
Connection Mode: Read / Write
Host Address: mockdb.internal.appsmith.com
Port: 5432
Database Name: yelp
User: yelp
Password: that-annoying-yelper
```

{% hint style="info" %}
To verify if this data source is valid or not, you can click on the `Test` button on your mid-bottom right. You should see a pop-up with the connection status.
{% endhint %}

Now, save your data source by clicking the **Save** button. You'll see a success pop-up on the top-right after successfully adding your DB.

### **Writing your First Query**

The data source is successfully connected; now, let's write a simple DB query to fetch all the business data from the business table. Follow the below steps to do so:

{% embed url="https://youtu.be/QoyzrOEG5to" %}
Running Queries on Appsmith
{% endembed %}

1. First, click on the `+` the icon next to the `Datasources`.
2. Find the created `Postgres Mock DB` data source under the Active tab and click `NEW QUERY`.
3. It will create a new DB Query that you can use across the Page.
4. Name this query as `getBusinessData` and click select.
5. Use the following query in the query pane to get all the business data:

```sql
select * from yelp_business;
```

To run this query, click on the **RUN** button in the top-right corner of the **DB query**.&#x20;

Just like that, you should see the response from the DB Query in the Response Pane tab below.&#x20;

Next, let's bind this data onto the powerful [table widget](https://docs.appsmith.com/widget-reference/table) of Appsmith!

{% hint style="info" %}
All names within a page must be unique, including widget names, query names, or API names.
{% endhint %}

### Binding Queries onto Widgets

In the previous section, you’ve created a DB query named **`getBusinessData`**; let's bind the query onto a table widget. You can achieve it in two ways:

The First and simple method is to open the query window and select the table option on the right-side property pane. It will automatically add a table widget to your canvas. The video below demonstrates adding a table widget from the query window.

{% embed url="https://youtu.be/XgQ9AsRdLek" %}
Adding a table widget from the query window
{% endembed %}

{% hint style="info" %}
Note that the above method would also automatically bind the data from the query for you.&#x20;
{% endhint %}

Let's look at another method for adding a table widget to your canvas.&#x20;

1. Click on the **`Widgets`** option from **entity explorer.**&#x20;
2. You'll find a great set of UI widgets here that you can use to build the application.
3. Drag and drop an **`Table widget`** onto the canvas.

{% hint style="info" %}
&#x20;Appsmith provides various widgets, like [tables](https://docs.appsmith.com/widget-reference/table), [lists](https://docs.appsmith.com/widget-reference/list), [buttons](https://docs.appsmith.com/widget-reference/button), [maps](https://docs.appsmith.com/widget-reference/maps), [audio](https://docs.appsmith.com/widget-reference/audio), [charts](https://docs.appsmith.com/widget-reference/chart), [forms](https://docs.appsmith.com/widget-reference/form), and more.
{% endhint %}

You'll notice a property window on the right side of the program as soon as you drag the widget into the canvas; you can call it the **Widget Property Pane**. All of the table's configurations and customization properties can be found here. Here's a screenshot of the table widget and its property pane:

![Appsmith Table Widget and Property Pane](../../.gitbook/assets/issue\_12550\_img3.png)

{% hint style="info" %}
You can access the docked property pane of any widget, by simply clicking on the widget from the canvas.
{% endhint %}

Let's look at the Table's Property Pane:

**Table Data**: To add data to the table, we can update the property pane's `Table Data` property. By default, it has some initial configuration; you can update it based on your preferences. But also make sure that it will only accept array data types. Go through the detailed documentation [here](https://docs.appsmith.com/widget-reference/table) To learn more about the table widget.

**Table Columns**: Beneath the Table Data property, you can configure all your column data. You can click on the cog icon and set the column data type individually.

{% hint style="info" %}
The table widget displays data in rows and columns. You can display data from an API in a table, trigger an action when a user selects a row, and even work with sizable paginated data sets.
{% endhint %}

These are the two fundamental properties needed for the table widget. However, many other properties allow you to add different actions and customize the UI. If you want to learn how to display data and handle pagination inside a table,[ read this guide. ](https://docs.appsmith.com/core-concepts/displaying-data-read/display-data-tables#pagination)

Now, in the **`Table Data`** property, let's bind the response from the DB Query. To do this, you'll have to use the Moustache Operator.

{% hint style="info" %}
In Appsmith, the mustache operator **`{{ /* This is JavaScript */ }}`** can be used anywhere to write JavaScript. For example, when binding data onto widgets, sending params to APIs, sharing data across pages, etc.
{% endhint %}

Now copy the following onto the `Table Data` property:

```javascript
{{ getBusinessData.data  }}
```

When you copy this onto the Table Data, you should see the data magically populated onto the table. Then, based on your preference, you can customize the column names and style your table widget with the other properties. The video below demonstrates how to add the table widget and fetch the data.

{% embed url="https://youtu.be/Ys1zN2GjNGA" %}
Adding a table widget to the canvas
{% endembed %}

But what just happened here?

Here, we are accessing the entire query object using the query name **`getBusinessData`**, and the **`.data`** property allows us to attach data.

Setting Table Data to **`{{ getBusinessData.data }}`** also ensures that whenever the Business Page loads, getBusinessData runs automatically. However, you can change this default behavior by toggling the field **"Run query on page load" in the Setting tab of getBusinessData.**

### What's Next?

You'll see in the next section that the inverse of this is also possible, and a query can also access i.e. a widget's state. Furthermore, all the building blocks of an Appsmith page - Widgets, DB Queries, and APIs can access each other's data and or state using their names.
