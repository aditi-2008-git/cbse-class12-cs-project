def func(suffix):
    fashiontb = 'fashion_pro_'+str(suffix)
    generaltb = 'general_pro_'+str(suffix)
    supplytb = 'supply_tb_'+str(suffix)
    customertb = 'customer_tb_' + str(suffix)
    while True:
        print('Tables')
        print('1. Fashion Products')
        print('2. General Products')
        print('3. Supply Table')
        print('4. Customer Table')

        ch = input('Enter which table would you like to work on (Type E to exit) : ')
        if ch in 'Ee':
            break

        while True:
            print()
            n1 = input('Do you want to insert(I), update(U), delete(D), show(S) or back(B)? : ')
            print()

            if n1 in 'Ii':
                while True:
                    if ch == '1':
                        com = input('Enter the company name (-- type B if want to get back --) : ')
                        if com in 'Bb':
                            break
                        cat = input('Enter the category name : ')
                        size = input('Enter the size : ')
                        mycur.execute(
                            "select * from " + fashiontb + " where company=%s and category=%s and size=%s",
                            (com, cat, size)
                        )
                        a = mycur.fetchone()
                        if a is not None:
                            print('Record already exists (Composite key violation)')
                            continue
                        qty = int(input('Enter the quantity : '))
                        pft = int(input('Enter profit per product(in rupees) : '))
                        mycur.execute(
                            "insert into " + fashiontb + " values (%s,%s,%s,%s,%s)",
                            (com, cat, size, qty, pft)
                        )
                        print()

                    elif ch == '2':
                        com = input('Enter the company name (-- type B if want to get back --) : ')
                        if com in 'Bb':
                            break
                        cat = input('Enter the category name : ')
                        exp = input('Enter the expiry date : ')
                        mycur.execute(
                            "select * from " + generaltb + " where company=%s and category=%s and expiry_date=%s",
                            (com, cat, exp)
                        )
                        a = mycur.fetchone()
                        if a is not None:
                            print('Record already exists (Composite key violation)')
                            continue
                        qty = int(input('Enter the quantity : '))
                        pft = int(input('Enter profit per product(in rupees) : '))
                        mycur.execute(
                            "insert into " + generaltb + " values (%s,%s,%s,%s,%s)",
                            (com, cat, exp, qty, pft)
                        )
                        print()

                    elif ch == '3':
                        order_no = int(input('Enter the order number (-- type 0 if want to get back --) : '))
                        if order_no == 0:
                            break
                        mycur.execute(
                            "select * from " + supplytb + " where order_no=%s",
                            (order_no,)
                        )
                        a = mycur.fetchone()
                        if a is not None:
                            print('Record already exists')
                            continue
                        pft = int(input('Enter the profit earned : '))
                        date_ord = input('Enter the date of order : ')
                        exp_del = input('Enter the expected delivery date : ')
                        spt = input('Enter the shipment date (Type N if not done yet) : ')
                        if spt not in 'Nn':
                            delv = input('Enter the delivery date (Type N if not done yet) : ')
                            if delv not in 'Nn':
                                mycur.execute(
                                    "insert into " + supplytb + " values (%s,%s,%s,%s,%s,%s)",
                                    (order_no, pft, date_ord, exp_del, spt, delv)
                                )
                            else:
                                mycur.execute(
                                    "insert into " + supplytb +
                                    " (order_no,profit,date_order,expected_delivery,shipment) values (%s,%s,%s,%s,%s)",
                                    (order_no, pft, date_ord, exp_del, spt)
                                )
                        else:
                            mycur.execute(
                                "insert into " + supplytb +
                                " (order_no,profit,date_order,expected_delivery) values (%s,%s,%s,%s)",
                                (order_no, pft, date_ord, exp_del)
                            )
                        print()

                    elif ch == '4':
                        order_no = int(input('Enter the order number (-- type 0 if want to get back --) : '))
                        if order_no == 0:
                            break
                        mycur.execute(
                            "select * from " + supplytb + " where order_no=%s",
                            (order_no,)
                        )
                        a = mycur.fetchone()
                        if a is None:
                            print('This order number doesn\'t exist')
                            continue

                        mycur.execute(
                            "select * from " + customertb + " where order_no=%s",
                            (order_no,)
                        )
                        a = mycur.fetchone()
                        if a is not None:
                            print('Record already exists ')

                        name = input('Enter customer name : ')
                        contact = int(input('Enter contact number : '))
                        add = input('Enter customer address : ')
                        mycur.execute(
                            "insert into " + customertb + " values (%s,%s,%s,%s)",
                            (order_no, name, contact, add)
                        )
                        print()

                    mydb.commit()

            elif n1 in 'Uu':
                while True:
                    if ch in '12':
                        print()
                        n2 = input('Do you want to update quantity(Q)  or profit(P) or Back(B) : ')
                        print()

                        if n2 in 'Qq':
                            com = input('Enter the existing company name  : ')
                            cat = input('Enter the category name : ')

                            if ch == '1':
                                size = input('Enter the size : ')
                                mycur.execute(
                                    "select * from " + fashiontb + " where company=%s and category=%s and size=%s",
                                    (com, cat, size)
                                )
                                a = mycur.fetchone()
                                if a is None:
                                    print('No such record exists')
                                else:
                                    qty = int(input('Enter the quantity to be updated : '))
                                    mycur.execute(
                                        "update " + fashiontb + " set quantity=%s where company=%s and category=%s and size=%s",
                                        (qty, com, cat, size)
                                    )
                            else:  # ch == '2'
                                exp = input('Enter the expiry date : ')
                                mycur.execute(
                                    "select * from " + generaltb + " where company=%s and category=%s and expiry_date=%s",
                                    (com, cat, exp)
                                )
                                a = mycur.fetchone()
                                if a is None:
                                    print('No such record exists')
                                else:
                                    qty = int(input('Enter the quantity to be updated : '))
                                    mycur.execute(
                                        "update " + generaltb + " set quantity=%s where company=%s and category=%s and expiry_date=%s",
                                        (qty, com, cat, exp)
                                    )
                            print('UPDATED')

                        elif n2 in 'Pp':
                            com = input('Enter the existing company name  : ')
                            cat = input('Enter the category name : ')

                            if ch == '1':
                                size = input('Enter the size : ')
                                mycur.execute(
                                    "select * from " + fashiontb + " where company=%s and category=%s and size=%s",
                                    (com, cat, size)
                                )
                                a = mycur.fetchone()
                                if a is None:
                                    print('No such record exists')
                                else:
                                    pft = int(input('Enter the profit to be updated : '))
                                    mycur.execute(
                                        "update " + fashiontb + " set profit_per_item=%s where company=%s and category=%s and size=%s",
                                        (pft, com, cat, size)
                                    )
                            else:  # ch == '2'
                                exp = input('Enter the expiry date : ')
                                mycur.execute(
                                    "select * from " + generaltb + " where company=%s and category=%s and expiry_date=%s",
                                    (com, cat, exp)
                                )
                                a = mycur.fetchone()
                                if a is None:
                                    print('No such record exists')
                                else:
                                    pft = int(input('Enter the profit to be updated : '))
                                    mycur.execute(
                                        "update " + generaltb + " set profit_per_item=%s where company=%s and category=%s and expiry_date=%s",
                                        (pft, com, cat, exp)
                                    )
                            print('UPDATED')

                    elif ch == '3':
                        print()
                        n2 = input('Do you want to update shipment date(S)  or delivery date(D) or Both (SD) or Back(B) : ').lower()
                        print()
                        order_no = int(input('Enter the order number : '))

                        mycur.execute(
                            "select * from " + supplytb + " where order_no=%s",
                            (order_no,)
                        )
                        a = mycur.fetchone()
                        if a is None:
                            print('No such record exists')
                            continue

                        if n2 == 's':
                            spt = input('Enter the shipment date : ')
                            mycur.execute(
                                "update " + supplytb + " set shipment=%s where order_no=%s",
                                (spt, order_no)
                            )
                        elif n2 == 'd':
                            delv = input('Enter the delivery date : ')
                            mycur.execute(
                                "update " + supplytb + " set delivery=%s where order_no=%s",
                                (delv, order_no)
                            )
                        elif n2 == 'sd':
                            spt = input('Enter the shipment date : ')
                            delv = input('Enter the delivery date : ')
                            mycur.execute(
                                "update " + supplytb + " set shipment=%s, delivery=%s where order_no=%s",
                                (spt, delv, order_no)
                            )
                        elif n2 in 'Bb':
                            break
                        print('UPDATED')
                        

                    elif ch == '4':
                        order_no = int(input('Enter the order number (Type 0 to get back) : '))
                        if order_no == 0:
                            break

                        mycur.execute(
                            "select * from " + supplytb + " where order_no=%s",
                            (order_no,)
                        )
                        a = mycur.fetchone()
                        if a is None:
                            print('No such record exists in supply table')
                        else:
                            add = input('Enter the new address  : ')
                            mycur.execute(
                                "update " + customertb + " set address=%s where order_no=%s",
                                (add, order_no)
                            )
                        print('UPDATED')

                    mydb.commit()


            elif n1 in 'Dd':
                print('Enter the details of record to be deleted : ')
                print()

                if ch == '1':
                    com = input('Enter the existing company name  : ')
                    cat = input('Enter the category name : ')
                    size = input('Enter the size : ')
                    mycur.execute(
                        "select * from " + fashiontb + " where company=%s and category=%s and size=%s",
                        (com, cat, size)
                    )
                    a = mycur.fetchone()
                    if a is None:
                        print('No such record exists')
                    else:
                        mycur.execute(
                            "delete from " + fashiontb + " where company=%s and category=%s and size=%s",
                            (com, cat, size)
                        )

                elif ch == '2':
                    com = input('Enter the existing company name  : ')
                    cat = input('Enter the category name : ')
                    exp = input('Enter the expiry date : ')
                    mycur.execute(
                        "select * from " + generaltb + " where company=%s and category=%s and expiry_date=%s",
                        (com, cat, exp)
                    )
                    a = mycur.fetchone()
                    if a is None:
                        print('No such record exists')
                    else:
                        mycur.execute(
                            "delete from " + generaltb + " where company=%s and category=%s and expiry_date=%s",
                            (com, cat, exp)
                        )

                elif ch == '3':
                    order_no = int(input('Enter the order number : '))
                    mycur.execute(
                        "select * from " + supplytb + " where order_no=%s",
                        (order_no,)
                    )
                    a = mycur.fetchone()
                    if a is None:
                        print('No such record exists')
                    else:
                        mycur.execute(
                            "delete from " + supplytb + " where order_no=%s",
                            (order_no,)
                        )

                elif ch == '4':
                    print('Records can\'t be deleted from here\nOnly record deletion from supply table would lead to record deletion here')
                print('DELETED\n')

                mydb.commit()


            elif n1 in 'Ss':
                new = input("Show full table (W) or apply conditions (P)? : ")
                print()

                if ch == '1':  # fashion_pro_1
                    if new in 'Ww':
                        mycur.execute("SELECT * FROM " + fashiontb)
                        rows = mycur.fetchall()
                        for row in rows:
                            print(row)
                    elif new in 'Pp':
                        query = "SELECT * FROM " + fashiontb + " WHERE "
                        com = input("Company (N if skip): ")
                        if com not in 'Nn':
                            query += "company = '" + com + "' AND "
                        cat = input("Category (N if skip): ")
                        if cat not in 'Nn':
                            query += "category = '" + cat + "' AND "
                        size = input("Size (N if skip): ")
                        if size not in 'Nn':
                            query += "size = '" + size + "' AND "
                        qty = input("Quantity condition (>/</= etc, N if skip): ")
                        if qty not in 'Nn':
                            query += "quantity " + qty + " AND "
                        pft = input("Profit condition (>/</= etc, N if skip): ")
                        if pft not in 'Nn':
                            query += "profit_per_item " + pft
                        print()
                        query = query.rstrip(" AND ")
                        query = query.rstrip(" WHERE ")
                        mycur.execute(query)
                        rows = mycur.fetchall()
                        for row in rows:
                            print(row)

                elif ch == '2':  # general_pro_1
                    if new in 'Ww':
                        mycur.execute("SELECT * FROM " + generaltb)
                        rows = mycur.fetchall()
                        for row in rows:
                            print(row)
                    elif new in 'Pp':
                        query = "SELECT * FROM " + generaltb + " WHERE "
                        com = input("Company (N if skip): ")
                        if com not in 'Nn':
                            query += "company = '" + com + "' AND "
                        cat = input("Category (N if skip): ")
                        if cat not in 'Nn':
                            query += "category = '" + cat + "' AND "
                        exp = input("Expiry date (N if skip): ")
                        if exp not in 'Nn':
                            query += "expiry_date = '" + exp + "' AND "
                        qty = input("Quantity condition (>/</= etc, N if skip): ")
                        if qty not in 'Nn':
                            query += "quantity " + qty + " AND "
                        pft = input("Profit condition (>/</= etc, N if skip): ")
                        if pft not in 'Nn':
                            query += "profit_per_item " + pft
                        print()
                        query = query.rstrip(" AND ")
                        query = query.rstrip(" WHERE ")
                        mycur.execute(query)
                        rows = mycur.fetchall()
                        for row in rows:
                            print(row)

                elif ch == '3':  # supply_tb_1
                    if new in 'Ww':
                        mycur.execute("SELECT * FROM " + supplytb)
                        rows = mycur.fetchall()
                        for row in rows:
                            print(row)
                    elif new in 'Pp':
                        query = "SELECT * FROM " + supplytb + " WHERE "
                        order_no = input("Order number (N if skip): ")
                        if order_no not in 'Nn':
                            query += "order_no = '" + order_no + "' AND "
                        date_ord = input("Order date condition (>/</= etc, N if skip): ")
                        if date_ord not in 'Nn':
                            query += "date_order " + date_ord + " AND "
                        exp_del = input("Expected delivery condition (>/</= etc, N if skip): ")
                        if exp_del not in 'Nn':
                            query += "expected_delivery " + exp_del + " AND "
                        spt = input("Shipment date condition (>/</= etc, N if skip): ")
                        if spt not in 'Nn':
                            query += "shipment " + spt + " AND "
                        delv = input("Delivery date condition (>/</= etc, N if skip): ")
                        if delv not in 'Nn':
                            query += "delivery " + delv + " AND "
                        print()
                        query = query.rstrip(" AND ")
                        query = query.rstrip(" WHERE ")
                        mycur.execute(query)
                        rows = mycur.fetchall()
                        for row in rows:
                            print(row)

                elif ch == '4':  # customer_tb_1
                    if new in 'Ww':
                        mycur.execute("SELECT * FROM " + customertb)
                        rows = mycur.fetchall()
                        for row in rows:
                            print(row)
                    elif new in 'Pp':
                        query = "SELECT * FROM " + customertb + " WHERE "
                        order_no = input("Order number (N if skip): ")
                        if order_no not in 'Nn':
                            query += "order_no = '" + order_no + "' AND "
                        name = input("Customer name (N if skip): ")
                        if name not in 'Nn':
                            query += "name = '" + name + "' AND "
                        contact = input("Contact (N if skip): ")
                        if contact not in 'Nn':
                            query += "contact = '" + contact + "' AND "
                        address = input("Address (N if skip): ")
                        if address not in 'Nn':
                            query += "address = '" + address + "' AND "
                        print()
                        query = query.rstrip(" AND ")
                        query = query.rstrip(" WHERE ")
                        mycur.execute(query)
                        rows = mycur.fetchall()
                        for row in rows:
                            print(row)

            elif n1 in 'Bb':
                break
            else:
                print('Invalid Choice, please select I, U, D, S, or B')


def data(t):
    l1 = []
    mycur.execute("select count(*), sum(profit) from supply_tb_1 where month(order_date)=%s and year(order_date)=%s",(t[0], t[1]))
    a = mycur.fetchone()
    l1.extend(a)

    mycur.execute("select count(*) from supply_tb_1 where expected_delivery < delivery and month(order_date)=%s and year(order_date)=%s",(t[0], t[1]))
    b = mycur.fetchone()
    l1.append((b[0] / a[0]) * 100 if a[0] != 0 else 0)

    l2 = []
    mycur.execute("select count(*), sum(profit) from supply_tb_2 where month(order_date)=%s and year(order_date)=%s",(t[0], t[1]))
    a = mycur.fetchone()
    l2.extend(a)

    mycur.execute("select count(*) from supply_tb_2 where expected_delivery < delivery and month(order_date)=%s and year(order_date)=%s",(t[0], t[1]))
    b = mycur.fetchone()
    l2.append((b[0] / a[0]) * 100 if a[0] != 0 else 0)

    l3 = []
    mycur.execute("select count(*), sum(profit) from supply_tb_3 where month(order_date)=%s and year(order_date)=%s",(t[0], t[1]))
    a = mycur.fetchone()
    l3.extend(a)

    mycur.execute("select count(*) from supply_tb_3 where expected_delivery < delivery and month(order_date)=%s and year(order_date)=%s",(t[0], t[1]))
    b = mycur.fetchone()
    l3.append((b[0] / a[0]) * 100 if a[0] != 0 else 0)

    fdate = '2025-'+str(t[0])+'-01'
    mycur.execute("select monthname(%s)", (fdate,))
    c = mycur.fetchone()

    flist = []
    flist.append([c[0], "unitR", "unitC", "unitD"])
    flist.append(["Total order", l1[0], l2[0], l3[0]])
    flist.append(["Total profit", l1[1], l2[1], l3[1]])
    flist.append(["Delay %age ", round(l1[2],2), round(l2[2],2), round(l3[2],2)])

    return flist

import mysql.connector
import csv
mydb = mysql.connector.connect(host = 'localhost', user = 'root', passwd = '12345', database = 'Push_Corporations')
mycur = mydb.cursor()
while True:
    login = input('Enter your login ID : ')
    psd = input('Enter your password  : ')

    if login == 'Push Corporate Raipur' and psd == 'Raipur_Manager':
        func(1)
    elif login == 'Push Corporate Chattisgarh' and  psd == 'Chattisgarh_Manager':
        func(2)

    elif login == 'Push Corporate Delhi' and psd == 'Delhi_Manager':
        func(3)

    elif login == 'Push Corporate SM' and psd == 'Manager_Senior':
        while True:
            print('''1. Business Overview
2. Delayed Orders
3. Save and Export
4. Exit ''')
            ch = int(input('Enter your choice : '))
            
            if ch == 1:
                mycur.execute("select month(curdate()), year(curdate())")
                t1 = mycur.fetchone()

                if t1[0] == 1:
                    t2 = (12, t1[1] - 1)
                    t3 = (11, t1[1] - 1)

                elif t1[0] == 2:
                    t2 = (1, t1[1])
                    t3 = (12, t1[1] - 1)

                else:
                    t2 = (t1[0] - 1, t1[1])
                    t3 = (t2[0] - 1, t1[1])
                for d in (data(t1), data(t2), data(t3)):
                    for i in d:
                        for j in i:
                            print(j, '\t\t', end='')
                        print()
                    print('\n')

            elif ch == 2:
                delay = int(input('How much dealyed orders to show : '))
                mycur.execute("select order_no,'Raipur', datediff(delivery, expected_delivery) from supply_tb_1 where delivery > expected_delivery and datediff(delivery, expected_delivery) > %s",(delay,))
                print('Order_no\tUnit\t\t Delay by')
                a = mycur.fetchall()
                for i in a:
                    print(i[0],'\t',i[1],'\t',i[2])

                mycur.execute("select order_no, 'Chattisgarh',datediff(delivery, expected_delivery) from supply_tb_2 where delivery > expected_delivery and datediff(delivery, expected_delivery) > %s",(delay,))
                a = mycur.fetchall()
                for i in a:
                    print(i[0],'\t',i[1],'\t',i[2])

                mycur.execute("select order_no, 'Delhi',datediff(delivery, expected_delivery) from supply_tb_3 where delivery > expected_delivery and datediff(delivery, expected_delivery) > %s",(delay,))
                a = mycur.fetchall()
                for i in a:
                    print(i[0],'\t',i[1],'\t',i[2])

            elif ch == 3:
                n1 = input('Do you want to save in file of previous three months(D), or custom ramge(C) or back(B):')
                if n1 in 'Bb':
                           continue
                filename = input("Enter thr filename to be save :")
                if not filename.endswith(".csv"):
                    filename+= ".csv"

                mycur.execute("select month(curdate()), year(curdate())")
                t1 = mycur.fetchone()

                if n1 in 'Dd':
                    if t1[0] == 1:
                        t2 = (12, t1[1] - 1)
                        t3 = (11, t1[1] - 1)

                    elif t1[0] == 2:
                        t2 = (1, t1[1])
                        t3 = (12, t1[1] - 1)

                    else:
                        t2 = (t1[0] - 1, t1[1])
                        t3 = (t2[0] - 1, t1[1])

                    with open(filename, "a",newline="" ) as file:
                        writer =  csv.writer(file)
                        mycur.execute('select curdate()')
                        a = mycur.fetchone()
                        writer.writerow(a)
                        writer.writerows(data(t1))
                        writer.writerows(data(t2))
                        writer.writerows(data(t3))
                        print('SAVED')

                elif n1 in 'Cc':
                    start = input("Enter start date (YYYY-MM-DD):")
                    end =  input("Enter end date (YYYY-MM-DD):")
                    l1 = []
                    mycur.execute("select count(*), sum(profit) from supply_tb_1 where order_date between %s and %s",(start,end))
                    a = mycur.fetchone()
                    l1.extend(a)
                    l1.insert(0,'Raipur')

                    mycur.execute("select count(*) from supply_tb_1 where order_date between %s and %s and delivery > expected_delivery",(start,end))
                    b = mycur.fetchone()
                    l1.append((b[0] / a[0]) * 100 if a[0] != 0 else 0)

                    l2 = []
                    mycur.execute("select count(*), sum(profit) from supply_tb_2 where order_date between %s and %s",(start,end))
                    a = mycur.fetchone()
                    l2.extend(a)
                    l2.insert(0,'Chattisgarh')

                    mycur.execute("select count(*) from supply_tb_2 where order_date between %s and %s and delivery > expected_delivery",(start,end))
                    b = mycur.fetchone()
                    l2.append((b[0] / a[0]) * 100 if a[0] != 0 else 0)

                    l3 = []
                    mycur.execute("select count(*), sum(profit) from supply_tb_3 where order_date between %s and %s",(start,end))
                    a = mycur.fetchone()
                    l3.extend(a)
                    l3.insert(0,'Delhi')

                    mycur.execute("select count(*) from supply_tb_3 where order_date between %s and %s and delivery > expected_delivery",(start,end))
                    b = mycur.fetchone()
                    l3.append((b[0] / a[0]) * 100 if a[0] != 0 else 0)

                    with open(filename,"a",newline='') as file:
                                  writer = csv.writer(file)
                                  writer.writerow(['Units','Total orders','Total profit','Delay %age'])
                                  writer.writerow(l1)
                                  writer.writerow(l2)
                                  writer.writerow(l3)

    else :
        print('No User Detected')






            
