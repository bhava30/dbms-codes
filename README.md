# dbms-codes
MASTER AND TRANSACTION TABLE:

-->CREATE TABLE Customers ( CustomerID INT PRIMARY KEY, name VARCHAR(255), Email VARCHAR(255), Phone VARCHAR(20), Address VARCHAR(255) );

INSERT INTO Customers VALUES(1, 'John', 'john@gamil.com', '1234567890', '123 Main St');

INSERT INTO Customers VALUES(2, 'Mary', 'mary@gmail.com', '2345678901', '456 Elm St');

INSERT INTO Customers VALUES(3, 'Luna', 'luna03@gamil.com', '9067875879', '890 Ally St');

INSERT INTO Customers VALUES (4, 'Lia', 'lia33@gamil.com', '8979598068', '908 Winter Way St');

INSERT INTO Customers VALUES(5, 'Luka', 'luka2009@gamil.com', '7869897859', '500 Anchor Avenue');


UPDATE Customers
SET Email = 'johnK@gmail.com'
WHERE CustomerID = 1;

DELETE FROM Customers
WHERE CustomerID = 3;




-->CREATE TABLE Drivers ( DriverID INT PRIMARY KEY, DriverName VARCHAR(255), LicenseNumber VARCHAR(50), VehicleID INT, Rating DECIMAL(3, 2) );

INSERT INTO Drivers VALUES(1, 'Leo', 'DL123456', 01, 4.5);

INSERT INTO Drivers VALUES(2, 'Alice', 'DL654321', 02, 4.8);

INSERT INTO Drivers VALUES(3, 'Code', 'DL564787', 03, 4.9);

INSERT INTO Drivers VALUES(4, 'Iris', 'DL786785', 04, 4.4);

INSERT INTO Drivers VALUES(5, 'Milo', 'DL908796', 05, 4.0);

select * from Drivers;

-->CREATE TABLE Vehicles ( VehicleID INT PRIMARY KEY, VehicleNumber VARCHAR(20), Type VARCHAR(50), Capacity INT );

INSERT INTO Vehicles VALUES(01, 'ABC123', 'Sedan', 4);

INSERT INTO Vehicles VALUES(02, 'XYZ789', 'SUV', 6);

INSERT INTO Vehicles VALUES(03, 'YZA564', 'Creta', 4);

INSERT INTO Vehicles VALUES(04, 'YUA890', 'Inova', 6);

INSERT INTO Vehicles VALUES(05, 'SUA450', 'Maruti', 4);

Select * from Vehicles;

-->CREATE TABLE Locations ( LocationID INT PRIMARY KEY, Name VARCHAR(255), Latitude DECIMAL(9, 6), Longitude DECIMAL(9, 6) );

INSERT INTO Locations VALUES(301, 'Lambeth', 40.7128, -74.0060);

INSERT INTO Locations VALUES(302, 'Merton', 34.0522, -118.2437);

INSERT INTO Locations VALUES(303, 'Redbridge', 48.8581, 31.1312);

INSERT INTO Locations VALUES(305, 'Westminster', 30.7863, -40.0987);

INSERT INTO Locations VALUES(304, 'HollywoodJunction', 20.8976, -37.0987);

Select * from Locations

-->CREATE TABLE PaymentMethods ( PaymentMethodID INT PRIMARY KEY, UserID INT, Type VARCHAR(50), Details VARCHAR(255) );


INSERT INTO PaymentMethods VALUES(101, 1, 'Credit Card', '********1234');

INSERT INTO PaymentMethods VALUES(102, 2, 'Cash', 'Pay in cash upon ride completion');

INSERT INTO PaymentMethods VALUES(103, 3, 'Cash', 'Pay in cash upon ride completion');

INSERT INTO PaymentMethods VALUES(104, 4, 'UPI', '8979598068');

INSERT INTO PaymentMethods VALUES(105, 5, 'Cash', 'Pay in cash upon ride completion');


Select * from PaymentMethods;

-->CREATE TABLE RideRequests ( RequestID INT PRIMARY KEY, CustomerID INT, PickupLocationID INT, DropoffLocationID INT, VehicleID INT, Status VARCHAR(50), FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID), FOREIGN KEY (PickupLocationID) REFERENCES Locations (LocationID), FOREIGN KEY (DropoffLocationID) REFERENCES Locations (LocationID), FOREIGN KEY (VehicleID) REFERENCES Vehicles (VehicleID)

);

INSERT INTO RideRequests VALUES (1, 1, 301, 302, 1, 'Pending');

INSERT INTO RideRequests VALUES (2, 2, 302, 301, 2, 'Ride Completed');

INSERT INTO RideRequests VALUES (3, 3, 303, 304, 3, 'Pending');

INSERT INTO RideRequests VALUES (4, 4, 304, 303, 4, 'Pending');

INSERT INTO RideRequests VALUES (5, 5, 305, 301, 5, 'Ride Completed');

Select * from RideRequests

-->CREATE TABLE RideAssignments ( AssignmentID INT PRIMARY KEY, DriverID INT, RequestID INT, Status VARCHAR(50), FOREIGN KEY (DriverID) REFERENCES Drivers (DriverID), FOREIGN KEY (RequestID) REFERENCES RideRequests(RequestID)

);

INSERT INTO RideAssignments VALUES (1, 1, 1, 'Assigned');

INSERT INTO RideAssignments VALUES (2, 2, 2, 'Assigned');

INSERT INTO RideAssignments VALUES (3, 3, 3, 'Assigned');

INSERT INTO RideAssignments VALUES (4, 4, 4, 'Assigned');

INSERT INTO RideAssignments VALUES (5, 5, 5, 'Assigned');

Select * from RideAssignments

-->CREATE TABLE RidePayments ( PaymentID INT PRIMARY KEY, CustomerID INT, DriverID INT, RideID INT, Amount DECIMAL(10, 2), FOREIGN KEY (CustomerID) REFERENCES Customers (CustomerID), FOREIGN KEY (DriverID) REFERENCES Drivers (DriverID), FOREIGN KEY (RideID) REFERENCES RideAssignments(AssignmentID) );

INSERT INTO RidePayments VALUES (1, 1, 1, 1, 200);

INSERT INTO RidePayments VALUES (2, 2, 2, 2, 250);

INSERT INTO RidePayments VALUES (3, 3, 3, 3, 300);

INSERT INTO RidePayments VALUES (4, 4, 4, 4, 350);

INSERT INTO RidePayments VALUES (5, 5, 5, 5, 400);

Select * from RidePayments

-->CREATE TABLE IncidentReportss ( ReportID INT PRIMARY KEY, RideID INT, CustomerID INT, Description VARCHAR(255),FOREIGN KEY (CustomerID) REFERENCES Customers (CustomerID), FOREIGN KEY (RideID) REFERENCES RideAssignments(AssignmentID));

INSERT INTO IncidentReportss VALUES(1, 1, 1, 'Minor accident, no injuries');

INSERT INTO IncidentReportss VALUES(2, 2, 2, 'Lost item in the car');

INSERT INTO IncidentReportss VALUES (3, 3, 3, 'It was good');

INSERT INTO IncidentReportss VALUES(4, 4, 4, 'A little Delayed');

INSERT INTO IncidentReportss VALUES(5, 5, 5, 'It was good');

select * from IncidentReports

-->CREATE TABLE RideReviewss ( ReviewID INT PRIMARY KEY, RideID INT, CustomerID INT, Rating DECIMAL(3, 2), ReviewText VARCHAR(255), FOREIGN KEY (CustomerID) REFERENCES Customers (CustomerID), FOREIGN KEY (RideID) REFERENCES RideAssignmentss(AssignmentID)

);

INSERT INTO RideReviewss VALUES(1, 1, 1, 4.0, 'Good ride experience');

INSERT INTO RideReviewss VALUES(2, 2, 2, 4.2, 'Smooth journey');

INSERT INTO RideReviewss VALUES(3, 3, 3, 4.3, 'Good ride');

INSERT INTO RideReviewss VALUES(4, 4, 4, 4.0, 'A little delay');

INSERT INTO RideReviewss VALUES(5, 5, 5, 4.5, 'Good ride');

select * from RideReviewss

-->CREATE TABLE DriverReviewss ( ReviewID INT PRIMARY KEY, DriverID INT, CustomerID INT, Rating DECIMAL(3, 2), ReviewText VARCHAR(50), FOREIGN KEY (CustomerID) REFERENCES Customers (CustomerID), FOREIGN KEY (DriverID) REFERENCES Drivers (DriverID), FOREIGN KEY (ReviewID) REFERENCES RideReviewss(ReviewID)

);

INSERT INTO DriverReviewss VALUES(1, 1, 1, 4.5, 'Great driver!'); 

INSERT INTO DriverReviewss VALUES (2, 2, 2, 4.8, 'Excellent service!');

INSERT INTO DriverReviewss VALUES (3, 3, 3, 4.9, 'Excellent service!');

INSERT INTO DriverReviewss VALUES (4, 4, 4, 4.0, 'Great Driver');

INSERT INTO DriverReviewss VALUES(5, 5, 5, 4.5, 'Excellent service');

select * from DriverReviewss

PL/SQL:

-->CREATE OR REPLACE PROCEDURE GetCustomerInfo(p_customer_id IN INT) AS
    v_customer_name Customers.name%TYPE;
    v_customer_email Customers.email%TYPE;
BEGIN
    SELECT name, email INTO v_customer_name, v_customer_email
    FROM Customers
    WHERE CustomerID = p_customer_id;

    DBMS_OUTPUT.PUT_LINE('Customer Name: ' || v_customer_name);
    DBMS_OUTPUT.PUT_LINE('Customer Email: ' || v_customer_email);
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('Customer not found.');
END GetCustomerInfo;
/

-->CREATE OR REPLACE PROCEDURE InsertNewVehicle(
    p_vehicle_id IN INT,
    p_vehicle_number IN VARCHAR2,
    p_type IN VARCHAR2,
    p_capacity IN INT
) AS
BEGIN
    INSERT INTO Vehicles (VehicleID, VehicleNumber, Type, Capacity)
    VALUES (p_vehicle_id, p_vehicle_number, p_type, p_capacity);

    DBMS_OUTPUT.PUT_LINE('Vehicle inserted successfully.');
EXCEPTION
    WHEN DUP_VAL_ON_INDEX THEN
        DBMS_OUTPUT.PUT_LINE('Vehicle with the same ID already exists.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An error occurred: ' || SQLERRM);
END InsertNewVehicle;
/

-->CREATE OR REPLACE PROCEDURE UpdateDriverRating(
    p_driver_id IN INT,
    p_new_rating IN DECIMAL
) AS
BEGIN
    UPDATE Drivers
    SET Rating = p_new_rating
    WHERE DriverID = p_driver_id;

    DBMS_OUTPUT.PUT_LINE('Driver rating updated successfully.');
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('Driver not found.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An error occurred: ' || SQLERRM);
END UpdateDriverRating;
/

-->CREATE OR REPLACE PROCEDURE GetTotalPaymentAmount(
    p_customer_id IN INT,
    p_total_amount OUT DECIMAL
) AS
BEGIN
    SELECT SUM(Amount) INTO p_total_amount
    FROM RidePayments
    WHERE CustomerID = p_customer_id;

    DBMS_OUTPUT.PUT_LINE('Total Payment Amount: ' || p_total_amount);
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('Customer not found.');
END GetTotalPaymentAmount;
/

-->CREATE OR REPLACE PROCEDURE ProcessRidePayments AS
    v_payment_id RidePayments.PaymentID%TYPE;
    v_customer_id RidePayments.CustomerID%TYPE;
    v_amount RidePayments.Amount%TYPE;
    v_error_count INT := 0;
BEGIN
    FOR payment_rec IN (SELECT * FROM RidePayments) LOOP
        BEGIN
            -- Simulate processing logic
            IF payment_rec.Amount > 500 THEN
                -- Log an error for payments over 500
                DBMS_OUTPUT.PUT_LINE('Error: Payment ' || payment_rec.PaymentID || ' exceeds 500.');
                v_error_count := v_error_count + 1;
            END IF;

            -- Additional processing logic can be added here

        EXCEPTION
            WHEN OTHERS THEN
                DBMS_OUTPUT.PUT_LINE('An error occurred for payment ' || payment_rec.PaymentID || ': ' || SQLERRM);
                v_error_count := v_error_count + 1;
        END;
    END LOOP;

    DBMS_OUTPUT.PUT_LINE('Total errors encountered: ' || v_error_count);
END ProcessRidePayments;
/

-->CREATE OR REPLACE PROCEDURE ProcessRidePayments AS
    v_payment_id RidePayments.PaymentID%TYPE;
    v_customer_id RidePayments.CustomerID%TYPE;
    v_amount RidePayments.Amount%TYPE;
    v_error_count INT := 0;
BEGIN
    FOR payment_rec IN (SELECT * FROM RidePayments) LOOP
        BEGIN
            -- Simulate processing logic
            IF payment_rec.Amount > 500 THEN
                -- Log an error for payments over 500
                DBMS_OUTPUT.PUT_LINE('Error: Payment ' || payment_rec.PaymentID || ' exceeds 500.');
                v_error_count := v_error_count + 1;
            END IF;

            -- Additional processing logic can be added here

        EXCEPTION
            WHEN OTHERS THEN
                DBMS_OUTPUT.PUT_LINE('An error occurred for payment ' || payment_rec.PaymentID || ': ' || SQLERRM);
                v_error_count := v_error_count + 1;
        END;
    END LOOP;

    DBMS_OUTPUT.PUT_LINE('Total errors encountered: ' || v_error_count);
END ProcessRidePayments;
/

NESTED QUERIES:

SELECT CustomerID, name, Email, Phone,
    (SELECT COUNT(*) FROM RideRequests WHERE CustomerID = Customers.CustomerID) AS RideRequestCount
FROM Customers;

SELECT DriverID, DriverName, LicenseNumber, Rating,
    (SELECT VehicleNumber FROM Vehicles WHERE VehicleID = Drivers.VehicleID) AS VehicleNumber,
    (SELECT Type FROM Vehicles WHERE VehicleID = Drivers.VehicleID) AS VehicleType
FROM Drivers;

SELECT RequestID, Status,
    (SELECT Name FROM Locations WHERE LocationID = RideRequests.PickupLocationID) AS PickupLocation,
    (SELECT Name FROM Locations WHERE LocationID = RideRequests.DropoffLocationID) AS DropoffLocation
FROM RideRequests;

SELECT PaymentID, Amount,
    (SELECT name FROM Customers WHERE CustomerID = RidePayments.CustomerID) AS CustomerName,
    (SELECT DriverName FROM Drivers WHERE DriverID = RidePayments.DriverID) AS DriverName
FROM RidePayments;

CURSOR:

CREATE OR REPLACE PROCEDURE RetrieveCustomers IS
   CURSOR customer_cursor IS
      SELECT * FROM Customers;
   v_customer Customers%ROWTYPE;
BEGIN
   OPEN customer_cursor;
   LOOP
      FETCH customer_cursor INTO v_customer;
      EXIT WHEN customer_cursor%NOTFOUND;
      -- Process the data as needed
      DBMS_OUTPUT.PUT_LINE('Customer ID: ' || v_customer.CustomerID || ', Name: ' || v_customer.Name);
   END LOOP;
   CLOSE customer_cursor;
END RetrieveCustomers;
/

CREATE OR REPLACE PROCEDURE RetrieveRequestsAndCustomers IS
   CURSOR req_cust_cursor IS
      SELECT rr.RequestID, rr.Status, c.Name AS CustName
      FROM RideRequests rr
      LEFT JOIN Customers c ON rr.CustomerID = c.CustomerID;
   v_req_record req_cust_cursor%ROWTYPE;
BEGIN
   OPEN req_cust_cursor;
   LOOP
      FETCH req_cust_cursor INTO v_req_record;
      EXIT WHEN req_cust_cursor%NOTFOUND;
      -- Process the data as needed
      DBMS_OUTPUT.PUT_LINE('Request ID: ' || v_req_record.RequestID || ', Status: ' || v_req_record.Status || ', Customer: ' || v_req_record.CustName);
   END LOOP;
   CLOSE req_cust_cursor;
END RetrieveRequestsAndCustomers;
/

CREATE OR REPLACE PROCEDURE UpdateDriverRatings IS
   CURSOR driver_cursor IS
      SELECT * FROM Drivers;
BEGIN
   OPEN driver_cursor;
   LOOP
      FETCH driver_cursor INTO v_driver;
      EXIT WHEN driver_cursor%NOTFOUND;
      -- Update driver ratings as needed
      UPDATE Drivers SET Rating = Rating + 0.1 WHERE DriverID = v_driver.DriverID;
   END LOOP;
   CLOSE driver_cursor;
END UpdateDriverRatings;
/

CREATE OR REPLACE PROCEDURE ProcessRidePayments IS
   CURSOR payment_cursor IS
      SELECT * FROM RidePayments;
   v_payment RidePayments%ROWTYPE;
BEGIN
   OPEN payment_cursor;
   LOOP
      FETCH payment_cursor INTO v_payment;
      EXIT WHEN payment_cursor%NOTFOUND;
      -- Process ride payments as needed
      IF v_payment.Amount > 500 THEN
         DBMS_OUTPUT.PUT_LINE('Error: Payment ' || v_payment.PaymentID || ' exceeds 500.');
      END IF;
   END LOOP;
   CLOSE payment_cursor;
END ProcessRidePayments;
/

CREATE OR REPLACE PROCEDURE RetrieveDriverReviews IS
   CURSOR driver_review_cursor IS
      SELECT * FROM DriverReviewss;
   v_review DriverReviewss%ROWTYPE;
BEGIN
   OPEN driver_review_cursor;
   LOOP
      FETCH driver_review_cursor INTO v_review;
      EXIT WHEN driver_review_cursor%NOTFOUND;
      -- Process driver reviews as needed
      DBMS_OUTPUT.PUT_LINE('Review ID: ' || v_review.ReviewID || ', Rating: ' || v_review.Rating || ', Review Text: ' || v_review.ReviewText);
   END LOOP;
   CLOSE driver_review_cursor;
END RetrieveDriverReviews;
/

TRIGGER:

CREATE OR REPLACE TRIGGER update_driver_rating_trigger
BEFORE INSERT ON RideReviewss
FOR EACH ROW
BEGIN
    UPDATE Drivers
    SET Rating = (Rating + :NEW.Rating) / 2
    WHERE DriverID = :NEW.DriverID;
END;
/

CREATE OR REPLACE TRIGGER new_ride_request_trigger
AFTER INSERT ON RideRequests
FOR EACH ROW
BEGIN
    INSERT INTO RideAssignments (DriverID, RequestID, Status)
    VALUES (NULL, :NEW.RequestID, 'Pending');
END;
/

CREATE OR REPLACE TRIGGER payment_received_trigger
AFTER INSERT ON RidePayments
FOR EACH ROW
BEGIN
    UPDATE RideAssignments
    SET Status = 'Completed'
    WHERE AssignmentID = :NEW.RideID;
END;
/

CREATE OR REPLACE TRIGGER payment_received_trigger
AFTER INSERT ON RidePayments
FOR EACH ROW
BEGIN
    UPDATE RideAssignments
    SET Status = 'Completed'
    WHERE AssignmentID = :NEW.RideID;
END;
/

CREATE OR REPLACE TRIGGER review_feedback_trigger
BEFORE INSERT ON DriverReviewss
FOR EACH ROW
BEGIN
    IF :NEW.Rating < 4.0 THEN
        DBMS_OUTPUT.PUT_LINE('Driver received a low rating. Further action may be required.');
        -- Additional actions can be added here
    END IF;
END;
/

CREATE OR REPLACE TRIGGER review_feedback_trigger
BEFORE INSERT ON DriverReviewss
FOR EACH ROW
BEGIN
    IF :NEW.Rating < 4.0 THEN
        DBMS_OUTPUT.PUT_LINE('Driver received a low rating. Further action may be required.');
        -- Additional actions can be added here
    END IF;
END;
/

CREATE OR REPLACE TRIGGER review_feedback_trigger
BEFORE INSERT ON DriverReviewss
FOR EACH ROW
BEGIN
    IF :NEW.Rating < 4.0 THEN
        DBMS_OUTPUT.PUT_LINE('Driver received a low rating. Further action may be required.');
        -- Additional actions can be added here
    END IF;
END;
/

VIEW:
CREATE VIEW RideRequestLocations AS
SELECT
    rr.RequestID,
    rr.CustomerID,
    c.Name AS CustomerName,
    l1.Name AS PickupLocation,
    l2.Name AS DropoffLocation,
    rr.VehicleID,
    rr.Status AS RequestStatus
FROM RideRequests rr
JOIN Customers c ON rr.CustomerID = c.CustomerID
JOIN Locations l1 ON rr.PickupLocationID = l1.LocationID
JOIN Locations l2 ON rr.DropoffLocationID = l2.LocationID;

-- View to show details of ride assignments with driver and vehicle information
CREATE VIEW AssignedRides AS
SELECT
    ra.AssignmentID,
    ra.DriverID,
    d.DriverName,
    rr.RequestID,
    rr.CustomerID,
    c.Name AS CustomerName,
    ra.Status AS AssignmentStatus,
    v.VehicleNumber,
    v.Type AS VehicleType,
    v.Capacity AS VehicleCapacity
FROM RideAssignments ra
JOIN Drivers d ON ra.DriverID = d.DriverID
JOIN RideRequests rr ON ra.RequestID = rr.RequestID
JOIN Customers c ON rr.CustomerID = c.CustomerID
JOIN Vehicles v ON d.VehicleID = v.VehicleID;

-- View to display the count of completed rides for each customer
CREATE VIEW CompletedRidesCount AS
SELECT
    c.CustomerID,
    c.Name AS CustomerName,
    COUNT(cr.RequestID) AS CompletedRidesCount
FROM Customers c
LEFT JOIN CompletedRides cr ON c.CustomerID = cr.CustomerID
GROUP BY c.CustomerID, c.Name;

-- View to show the count of incident reports for each driver
CREATE VIEW DriverIncidentReportCount AS
SELECT
    d.DriverID,
    d.DriverName,
    COUNT(ir.ReportID) AS IncidentReportCount
FROM Drivers d
LEFT JOIN IncidentReportsView ir ON d.DriverID = ir.DriverID
GROUP BY d.DriverID, d.DriverName;

-- View to display the total earnings for each driver
CREATE VIEW DriverEarnings AS
SELECT
    d.DriverID,
    d.DriverName,
    SUM(rp.Amount) AS TotalEarnings
FROM Drivers d
JOIN RidePayments rp ON d.DriverID = rp.DriverID
GROUP BY d.DriverID, d.DriverName;
a


