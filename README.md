def get_order():
    item = input()
    if not item:
        return '00'
    if item == 'Q':
        return 'QQ'
    quantity = int(input('How many? '))
    return item, quantity
    
register = 0
order = ''
prices = 50, 75, 100

print('Coffee Station starting up...')
print('Ready to take orders!')

while 1:
    print('What would you like to order (1-3)? One at a time, please.')
    print('1. Espresso - $1.50\n'
          '2. Mocha - $3.85\n'
          '3. Cookie - $1.00'\n'
          '4. Cheese Cake - $5.00')
    item, quantity = get_order()
    if item == 'Q':
        break
    if item == '0':
        quantities = list(order.count(obj) for obj in '123')
        for name,number,price in zip(('Espresso', 'Mocha', 'Cookies', 'Cheese Cake' ),
                                       quantities,
                                       prices):
            if number:
                print('{}: {}. ${:.02f}'.format(name, number, number*price/100))
        total = sum(name*number for name,number in zip(quantities, prices))
        register += total
        print('Total: ${:.02f}'.format(total/100))
        tendered = int(input('Input cash (n.nn): ').replace('.', '').lstrip('0'))
        change = tendered - total
        denominations = ('Rm50', 'RM20', 'RM10', 'RM5', 'RM1',
                         '20SEN', '10SEN', '5SEN' )
        user_denominations = {}
        dollars, cents = divmod(change, 100)
        user_denominations['RM50'], dollars = divmod(dollars, 50)
        user_denominations['Rm20'], dollars = divmod(dollars, 20)
        user_denominations['RM10'], dollars = divmod(dollars, 10)
        user_denominations['RM5'], user_denominations['RM5'] = divmod(dollars, 5)
        user_denominations['20SEN'], cents = divmod(cents, 20)
        user_denominations['10SEN'], cents = divmod(cents, 10)
        user_denominations['5SEN'], user_denominations['5SEN'] = divmod(cents, 5)
        if any(user_denominations.values()):
            print('Your change:')
            for denomination in denominations:
                quant = user_denominations[denomination]
                if quant:
                    print('{}: {}'.format(denomination, quant))
        order = ''
    else:
        order += item*quantity

print("Today's total: ${:.02f}".format(register/100))
