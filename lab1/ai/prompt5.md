## Prompt
Read specs.md and edit ER-diagram yet again


## AI responce
I’ll compare the current spec against the diagram as it exists now, then make the smallest required update and check the Mermaid file for errors.

Read 

Read 

The new spec adds `user_id` and `address_id` to `ORDER`, and specifies that each order ships to exactly one address while an address can receive many orders. The diagram already links orders to users but omits both the order’s address field and address relationship, so I’ll add those directly.

Generating patch (15 lines) in 


```

```


Checked , no problems found

Updated `diagram.mmd` with `ORDER.address_id` and the one-to-many relationship from `ADDRESS` to `ORDER`. Validation reports no errors.

Made changes.