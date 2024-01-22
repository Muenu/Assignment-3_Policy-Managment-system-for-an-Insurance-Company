# Assignment-3_Policy-Managment-system-for-an-Insurance-Company

# Object -Oriented Programming concepts
This assignment was testing Object Oriented programming. It required an understanding of classes

#1. Create separate classses for policyholders,products and payments
#2. Policyholders Management: Implement methods to register, suspend and reactivate policyholders

class Policyholder:
    def __init__(self, id, name):
        self.id = id
        self.name = name
        self.status = "active"

    def suspend(self):
        self.status = "suspended"

    def reactivate(self):
        self.status = "active"

    def display_details(self):
        return f"Policyholder {self.name} - ID: {self.id}, Status: {self.status}"


#Product management
class Product:
    def __init__(self, product_id, name, price):
        self.product_id = product_id
        self.name = name
        self.price = price
        self.status = "active"


# Payment Management
class Payment:
    def __init__(self, policyholder, product, amount, date):
        self.policyholder = policyholder
        self.product = product
        self.amount = amount
        self.date = date
# 3. Payment Management: implement method for payment processing, reminders and penalties 
    def process_payment(self):
        if not self.product.status == "active":
            raise ValueError("Cannot process payment for inactive product")

        if not self.policyholder.status == "active":
            raise ValueError("Cannot process payment for suspended policyholder")

        # Add logic to process payment
        print(f"Payment of ${self.amount} processed for {self.policyholder.name} on {self.date}")

    def display_payment_details(self):
        return f"Payment Details - Policyholder: {self.policyholder.name}, Product: {self.product.name}, Amount: ${self.amount}, Date: {self.date}"


class ProductManager:
    products = []

    @classmethod
    def create_product(cls, product_id, name, price):
        product = Product(product_id, name, price)
        cls.products.append(product)
        return product

    @classmethod
    def update_product(cls, product, new_name, new_price):
        if not product.status == "active":
            raise ValueError("Cannot update inactive product")

        product.name = new_name
        product.price = new_price

    @classmethod
    def remove_product(cls, product):
        if not product.status == "active":
            raise ValueError("Cannot remove/suspend inactive product")

        product.status = "suspended"


# 5. Policyholder Demonstration
def demonstrate_policyholders():
    try:
        product_a = ProductManager.create_product(1, "Insurance Plan A", 1000)

        policyholder_1 = Policyholder(101, "Anne Rose")
        policyholder_2 = Policyholder(102, "James Carter")

        payment_1 = Payment(policyholder_1, product_a, 1000, "2024-01-22")
        payment_2 = Payment(policyholder_2, product_a, 1000, "2024-01-23")

        # Display Policyholder Account Details
        print(policyholder_1.display_details())
        payment_1.process_payment()
        print(payment_1.display_payment_details())

        print("\n")

        print(policyholder_2.display_details())
        payment_2.process_payment()
        print(payment_2.display_payment_details())

    except ValueError as e:
        print(f"Error: {e}")


if __name__ == "__main__":
    demonstrate_policyholders()
