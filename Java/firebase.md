```java
// fetch reference database
FirebaseDatabase mDatabase = FirebaseDatabase.getInstance();
DatabaseReference mDbRef = mDatabase.getReference("Donor/Name");
```



```java
// Write a message to the database
FirebaseDatabase mDatabase = FirebaseDatabase.getInstance();
DatabaseReference mDbRef = mDatabase.getReference("Donor/Name");
mDbRef.setValue("Parinitha Krishna");
```

```java
// Read from the database
mDbRef.addValueEventListener(new ValueEventListener() {
@Override
public void onDataChange(DataSnapshot dataSnapshot) {
// This method is called once with the initial value and again
        // whenever data at this location is updated.
String value = dataSnapshot.getValue(String.class);
        Log.d(TAG, "Value is: " + value);
    }

@Override
public void onCancelled(DatabaseError error) {
// Failed to read value
Log.w(TAG, "Failed to read value.", error.toException());
    }
});
```

```
