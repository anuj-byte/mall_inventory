import datetime
import pymongo
from pymongo import MongoClient 
client = MongoClient()
client 
class mall_screen:
    def __inint__(self):
        self._make = '' 
        self._iteam = ''
        self._year =0
        self._specification = ''
        self._feedback = '' 
    def add_iteam(self): 
        try:
            self._make = input('Enter product make : ')
            self._iteam = input('Enter product iteam : ') 
            self._year =input('enter product year: ') 
            self._specification = input('Enter specification: ')
            self._feedback = input('enter feedback: ')
            return True 
        except ValueError: 
            print('please try entering products date information again using only whole numbers for mileage and year') 
            return False 
    def __str__(self):
        return '\t'.join(str(a)for a in [self._make,self._iteam,self._year,self._specification,self._feedback])
class iteam_inventory: 
    def __init__(self):
        self.iteams = [] 
    def add_iteam(self):
        mall = mall_screen()
        if mall.add_iteam()== True:
            self.iteams.append(mall)
            print()
            print('this products has been added thank you') 
    def Display_iteam_inventory(self):
        print('\ta'.join(['','Make','Iteam','year','specification','feedback']))
        for idx, mall in enumerate(self.iteams):
            print(idx+1,end='\t') 
            print(mall) 
inventory = iteam_inventory() 
while True:

    print('choice 1:Add product to inventory')
    print('choice 2:Delete product from inventory')
    print('choice 3:view current inventory')
    print('choice 4:update product in inventory')
    print('choice 5: export current inventory')
    print('choice 6: Quit')
    User_choice=input('please enter your choice from one of the above option: ')
    if User_choice=="1":
        inventory.add_iteam()
    elif User_choice=='2':
        if len(inventory.iteams)<1:
            print('sorry there are no product currently in inventory')
            continue
        inventory.Display_iteam_inventory()
        products= int(input('please enter the number associated with the product to be removed: '))
        if products -1> len(inventory.iteams[products - 1]):
            print('this is a invalid number')

        else:
            inventory.iteams.remove(inventory.iteams[products -1])
            print_()
            print('this product has been removed')
    elif User_choice=='3':
        if len(inventory.iteams)<1:
            print('sorry there are no product currently available')
            continue
        inventory.Display_iteam_inventory()
    elif User_choice=='4':
        if len(inventory.iteams)<1:
            print('sorry there is no product')
            continue
        inventory.Display_iteam_inventory()
        products = int (input('please enter the number as which the vehicle is associated'))
        if products-1> len(inventory.iteams):
            print('this is an invalid number')
        else:
            auto_mall= mall_screen()
            if auto_mall.add_iteam() == True:
                inventory.iteams.remove(inventory.iteams[products-1])
                inventory.iteams.insert(products-1,auto_iteam)
                print_()
                print('this product has been updated')
    elif User_choice=='5':
        if len(inventory.iteams)<1:
            print('sorry there are no product currently available')
            continue
        db=client['inventory']
        cars= db['iteams']
        def add_iteam(make,iteam,date,specification,expired):
            document={
            'Make':make, 
            'Iteam':iteam, 
            'Date':date, 
            'Specification':specification, 
            'Expried':expired
            }   
            return iteam.insert_one(document)
            inventory.add_iteam()
            
        print('the vehicle inventory has been exported to the file')
    elif User_choice=='6':
        print('goodbye')
        break
    else:
        print('this is an invalid.please try again')
