-- Create the CUSTOMER table
CREATE TABLE CUSTOMER (
    CustomerID INT PRIMARY KEY,
    CustomerName VARCHAR2(100) NOT NULL,
    ContactName VARCHAR2(100),
    Address VARCHAR2(255),
    City VARCHAR2(100),
    PostalCode VARCHAR2(20),
    Country VARCHAR2(100)
);

-- Create the PRODUCT table
CREATE TABLE PRODUCT (
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR2(100) NOT NULL,
    SupplierID INT,
    CategoryID INT,
    QuantityPerUnit VARCHAR2(50),
    Price DECIMAL(10, 2),
    UnitsInStock INT,
    UnitsOnOrder INT,
    ReorderLevel INT,
    Discontinued CHAR(1) CHECK (Discontinued IN ('Y', 'N'))
);

-- Create the ORDER table
CREATE TABLE ORDERS (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    EmployeeID INT,
    OrderDate DATE DEFAULT SYSDATE,
    ShipperID INT,
    FOREIGN KEY (CustomerID) REFERENCES CUSTOMER(CustomerID)
);

-- Create the ORDER_DETAILS table
CREATE TABLE ORDER_DETAILS (
    OrderID INT,
    ProductID INT,
    Quantity INT,
    Price DECIMAL(10, 2),
    PRIMARY KEY (OrderID, ProductID),
    FOREIGN KEY (OrderID) REFERENCES ORDERS(OrderID),
    FOREIGN KEY (ProductID) REFERENCES PRODUCT(ProductID)
);

-- Create the SUPPLIER table
CREATE TABLE SUPPLIER (
    SupplierID INT PRIMARY KEY,
    SupplierName VARCHAR2(100) NOT NULL,
    ContactName VARCHAR2(100),
    Address VARCHAR2(255),
    City VARCHAR2(100),
    PostalCode VARCHAR2(20),
    Country VARCHAR2(100)
);

-- Create the CATEGORY table
CREATE TABLE CATEGORY (
    CategoryID INT PRIMARY KEY,
    CategoryName VARCHAR2(100) NOT NULL,
    Description VARCHAR2(255)
);
ALTER TABLE PRODUCT
ADD Category VARCHAR2(20);

ALTER TABLE ORDERS
ADD OrderDate DATE DEFAULT SYSDATE;
