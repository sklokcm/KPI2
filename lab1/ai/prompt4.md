## Prompt
Read specs.md and edit ER-diagram again

## AI responce
I’ll reread the latest spec and current diagram together, then adjust only what the new spec requires and validate the updated Mermaid file.

Read 

Read 

The latest spec adds a separate `ADDRESS` entity and says one user may have many addresses, with each address belonging to one user. The current diagram still stores `address` and `postcode` directly on `USER`, so I’ll replace those fields with the new entity and one-to-many relationship; the remaining listed entities and cardinalities already match.

Generating patch (25 lines) in 


```

```


Checked , no problems found

Updated `diagram.mmd` to add the `ADDRESS` entity and its one-to-many relationship with `USER`. Removed the address and postcode fields from `USER`; the diagram now reflects the latest spec. Validation reports no errors.

Made changes.