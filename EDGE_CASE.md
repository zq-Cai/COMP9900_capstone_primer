# Document your edge case here

1) The edge case you identified:
Invalid mark boundaries and missing optional fields. While the system allows the `mark` field to be optional (e.g., a student hasn't received a mark yet), if a user does provide a mark, it could be logically invalid (such as a negative number, a string, or a number greater than 100). 

2) How you have accounted for this in your implementation:
In the `app.py` implementation for both the `POST` and `PUT` methods, I added validation checks for the `mark` variable. 
- If `mark` is `None`, it is safely passed to the database (and ignored in the `/stats` calculation). 
- If `mark` is provided, the code attempts to cast it to an integer. If it fails, or if the value falls outside the `0` to `100` range, the API rejects the request and returns a `404` status code (as per the "all errors return 404" instruction for simplicity) rather than processing faulty data.