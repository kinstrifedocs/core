# Database Implementation Details

The database system is based on Unity's `ScriptableObject`, each entry in the database system 
is a ScriptableObject instance. In order to be identifiable via a GUID, database entry 
types must inherit from [IdentifiableObject](xref:Kinstrife.Identifier.IdentifiableObject), which
is a type of ScriptableObject that also contains a serializable, accessible GUID.

The database itself is essentially a giant `Dictionary<GUID, IdentifiableObject>`. 
The [DatabaseAccessor](xref:Kinstrife.Database.DatabaseAccessor) 
allows convenient retrieval of elements by [GUID](xref:Kinstrife.Identifier.Guid) and `type`. 
The [DatabaseLocator](xref:Kinstrife.Database.DatabaseLocator) locates folders/data paths that 
should be searched for database entries. For now, this only works for files in Resources/Datbase/
directories. Located database entries are injected into the database by the 
[DatabaseInjector](xref:Kinstrife.Database.DatabaseInjector), which also sorts entries for efficient
querying via type or interface filtering.