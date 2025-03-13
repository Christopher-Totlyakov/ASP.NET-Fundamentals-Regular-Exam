# Homework-ChristopherST-Regular Exam
# 🎓 [View certificate](https://softuni.bg/certificates/details/228266/c081d9d9)

Welcome to DeskMarket! DeskMarket is your go-to platform for the latest in technology. Whether you're looking for high-performance laptops, powerful workstations, or top-tier accessories, DeskMarket has everything you need to elevate your work and play.

# Table of Contents

1. [Identity Requirements](#identity-requirements)  
2. [Database Requirements](#database-requirements)  
3. [Page Requirements](#page-requirements)
5. [Functionality](#functionality)
6. [Security Requirements](#security-requirements)
7. [Code Quality](#code-quality)  
8. [Scoring](#scoring)  
9. [Installation](#installation)  

---

## Identity Requirements

- Scaffold Identity and use the default `IdentityUser`.
- Remove unnecessary code from the `Login.cshtml` and `Register.cshtml` files, leaving only the required code for functionality.
- **Password requirements**:
    - Require confirmed account: **false**
    - Require digits: **false**
    - Require non-alphanumeric characters: **false**
    - Require uppercase letters: **false**

## Database Requirements

### Entities:

#### Product:
- **Id** – unique integer, Primary Key.
- **ProductName** – string with min length 2 and max length 60 (required).
- **Description** – string with min length 10 and max length 250 (required).
- **Price** – decimal in range [1.00m; 3000.00m] (required).
- **ImageUrl** – nullable string (not required).
- **SellerId** – string (required).
- **Seller** – IdentityUser (required).
- **AddedOn** – DateTime with format `dd-MM-yyyy` (required).
- **CategoryId** – integer, foreign key (required).
- **Category** – Category (required).
- **IsDeleted** – bool (default value: false).
- **ProductsClients** – collection of type `ProductClient`.

#### Category:
- **Id** – unique integer, Primary Key.
- **Name** – string with min length 3 and max length 20 (required).
- **Products** – collection of type `Product`.

#### ProductClient:
- **ProductId** – integer, PrimaryKey, foreign key (required).
- **Product** – Product.
- **ClientId** – string, PrimaryKey, foreign key (required).
- **Client** – IdentityUser.

Implement the entities with the correct data types and relationships.

## Page Requirements

### Index Page:
- **Logged-out user**: Access to homepage and product index page.
  ![image](https://github.com/user-attachments/assets/d9fb3a02-1197-440f-bb72-cb3fdd47cd83)
   ![image](https://github.com/user-attachments/assets/22a8d900-1818-4074-ae02-79a5a3073506)

- **Logged-in user**: Redirected to `/Product/Index` after login.
![image](https://github.com/user-attachments/assets/c85f354f-ec50-4a06-a704-7f34c254a5e2)

### Login and Register Pages:
- **Logged-out user**: Access to login and register pages.
  ![image](https://github.com/user-attachments/assets/528ea0d8-2af1-41c0-b5c1-cc834cc2262f)
  ![image](https://github.com/user-attachments/assets/ccaa571a-2572-4c6a-82f1-c7dda802e7da)

### Product Pages:
- **/Product/Add**: Logged-in user only.
 
![image](https://github.com/user-attachments/assets/bb3704fa-e55f-42bd-9c70-06d3b3acbc99)

- **/Product/Index**: Logged-in user redirected to product index page.
![image](https://github.com/user-attachments/assets/8a4f6fd1-9216-4c09-84c6-e88db8cda9e5) 

- **/Product/Cart**: Logged-in user cart page.
- ![image](https://github.com/user-attachments/assets/51ec6efd-c21e-495b-8031-bc362349168e)

- **/Product/Edit/{id}**: Logged-in user editing their product only.
- ![image](https://github.com/user-attachments/assets/9d318af4-5f80-46f9-9b15-f8e7d55c9afc)

- **/Product/AddToCart?id={id}**: Adds selected product to user's cart (prevents duplicates).
  - This feature adds the selected product to the user's cart. If the product is already in the user's cart, it should not be added again. If the addition is successful, the users will be redirected to their cart page "/Product/Cart" page.
- **/Product/RemoveFromCart?id={id}**: Removes selected product from user's cart.
  - This feature removes the selected product from the user's cart. If the removal is successful, the user will be redirected to their cart page "/Product/Cart" page.
NOTE: The templates should look EXACTLY as shown above.
![image](https://github.com/user-attachments/assets/92b3a3e3-c075-4b16-a126-c85028cec83e)
![image](https://github.com/user-attachments/assets/b82081c6-2d5f-4553-a5cb-56009268b67c)

- **/Product/Details/{id}**: Product details page with different buttons depending on user role.
  - logged-in user, seller of a product
  ![image](https://github.com/user-attachments/assets/fe6259a5-b34f-41ad-a5d4-6f642415cb89)
  - logged-in user, not a seller of a product
![image](https://github.com/user-attachments/assets/d74afaac-62bb-4a6f-97f3-1c7fc5437155)
  - guest user, not logged-in
    ![image](https://github.com/user-attachments/assets/256e3e75-88ee-450f-b8a3-560a4f8ce87c)
    
- **Product/Delete/{id} (logged-in user, seller of a product)
  - When the logged-in user who is the seller of a product accesses this page, they will be able to initiate the deletion of a product. However, this is a soft delete process, meaning that the product will remain in the database but 
will no longer appear in the product listings. The product can no longer be bought or viewed by users, effectively removing it from the storefront.
After confirming the delete, the seller will be redirected to the product controller,  index action. This process is one-directional and irreversible through the user interface, as once deleted, the product will not be displayed in the system again unless manually restored through the database.
![image](https://github.com/user-attachments/assets/067ace66-b24f-4854-ac75-fd5d236bb364)
![image](https://github.com/user-attachments/assets/3a3909f2-ce87-42a5-8d28-0ee79fd1889a)
![image](https://github.com/user-attachments/assets/e6b9a7a7-7ea1-4bcd-976f-39a5f7cd61c2)
![image](https://github.com/user-attachments/assets/b92b4267-5538-4415-9875-ed41d01a46a9)
![image](https://github.com/user-attachments/assets/cc7854f8-9d37-4bdf-bd42-749cdfa69cc7)


### Security & Access Control:
- **Guest users**: Can access Home page, Product Index page, and Product Details page.
- **Logged-in users**: Can access `Product/Add`, `Product/Edit`, `Product/Cart`, and `Product/Index` pages.
- **Seller**: Can access the `Product/Edit` and `Product/Delete` pages for their products.

## Functionality

### User Features:
- **Guests**: Can register, log in, and view the homepage and product index page.
- **Logged-in users**: Can publish and edit products they own.
- **Product Details**:
    - **Guest users**: View product details, but cannot buy, edit, or delete.
    - **Logged-in users (Not the Seller)**: Can view the product details and buy, but cannot edit or delete.
    - **Sellers**: Can edit and delete their products, but cannot buy them.
  
### Product Features:
- **Add products**: Users can add new products.
- **View Products**: All products are visible on the homepage.
- **Cart**: Users can add products to their cart. Duplicate products are prevented.
- **Product Deletion**: Soft delete products from the storefront.

## Redirections:
- **Login**: Redirect to `/Product/Index` after successful login.
- **Product Add**: Redirect to `/Product/Index` after publishing a product.
- **Product Cart**: Redirect to `/Product/Index` after adding a product to the cart.
- **Product Edit**: Redirect to `/Product/Details/{product_id}` after successful editing.
- **Remove from Cart**: Redirect to `/Product/Cart` after successful removal.

## Security Requirements:
- **Guests**: Can access home, product index, product details, login, and register pages.
- **Users**: Logged-in users can access their dashboard, publish products, and edit their own products.
- **Redirection**: If logged-in users attempt to access restricted pages, they will be redirected accordingly.

## Code Quality
Ensure that your project follows good practices, SOLID principles, and proper architecture. Focus on structuring the code in a modular, scalable, and maintainable way.

## Scoring

- **Identity Requirements**: 5 points
- **Database Requirements**: 10 points
- **Template Requirements**: 10 points
- **Functionality**: 50 points
- **Security**: 5 points
- **Code Quality**: 10 points
- **Data Validation**: 10 points


## Installation
1.Clone the repository:
```bash
   git clone https://github.com/Christopher-Totlyakov/GameZone-ASP.NET-Fundamentals.git
```

### In Package Manager Console    
2.Install the dependencies: Ensure all required packages are installed by running the following command:
```bash
  dotnet restore
```
3.changes ConnectionStrings on yours in appsettings.json
4.migrate to MS SQL Server
```bash
  Update-Database
