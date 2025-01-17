---
group: graphql
title: Sales endpoint
---

The Sales module performs a wide variety of functions, including order, invoice, and shipment management. However, most of these functions are performed on the backend, and the customer does not have access to this information. The Sales endpoint allows a customers to retrieve their order histories.

## Query

The `customerOrders` query returns a list of customer orders.

Magento recommends you use customer tokens in the header of your GraphQL calls. However, you also can use [session authentication]({{ page.baseurl }}/get-started/authentication/gs-authentication-session.html).

### Syntax

`{customerOrders {CustomerOrders}}`

### Customer orders attributes

The `CustomerOrders` object contains the `items` attribute.

Attribute | Data type | Description
--- | --- | ---
`items` | [`[CustomerOrder]`](#customerOrderAttributes) | An array of customer orders

### Customer order items attributes {#customerOrderAttributes}

The `CustomerOrder` object defines details about each order the customer has placed.

Attribute | Data type | Description
--- | --- | ---
`created_at` | String | A timestamp indicating when the order was placed
`grand_total` | Float | The total of the order
`id` | Int | The ID assigned to the customer's order
`increment_id` | String | An ID that indicates the sequence of the order in the customer's order history
`status` | String | The status of the order, such as `open`, `processing`, or `closed`

## Example usage

The following query returns the order history of the logged in customer.

**Request**

```text
{
  customerOrders {
    items {
      increment_id
      id
      created_at
      grand_total
      status
    }
  }
}
```

**Response**

```json
{
  "data": {
    "customerOrders": {
      "items": [
        {
          "increment_id": "000000001",
          "id": 1,
          "created_at": "2019-02-21 00:24:34",
          "grand_total": 36.39,
          "status": "processing"
        },
        {
          "increment_id": "000000002",
          "id": 2,
          "created_at": "2019-02-21 00:24:35",
          "grand_total": 39.64,
          "status": "closed"
        }
      ]
    }
  }
}
```