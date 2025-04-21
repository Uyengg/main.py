import random

print("""
Escape тоглоомд тавтай морил.
Та их элсэн говийн дунд байдаг шоронгоос оргож байгаа ба зугтаахын тулд
харгалзагчийнхаа тэмээг хулгайлах болно.
Мэдээж хэрэг цагдаа нар таны араас хөөх ба 200км-ийн цаана байрлах нуувчиндаа хүрч
чадвал та аврагдах болно.
Таны эсэн мэнд зугтан гарах эсэх нь таны гаргах шийдвэрүүдээс хамаарах болно.
Танд амжилт хүсье.
""")

km_traveled = 0
thirst = 0
camel_tired = 0
police_traveled = -20
drinks = 5
done = False
hidden_event = False

# Зөвхөн тэмээ амрах үед хүнд үедээ зам туулна
camel_condition = 100

while not done:
    print("""
A. Ус уух
B. Дундаж хурдаар явах
C. Бүх хурдаараа явах
D. Зогсож амрах
E. Нөхцөл байдлыг шалгах
Q. Гарах
    """)
    choice = input("Таны сонголт? ").upper()

    if choice == "Q":
        print("Тоглоомоос гарлаа.")
        done = True

    elif choice == "E":
        print(f"Туулсан зам: {km_traveled} км")
        print(f"Савтай усны тоо: {drinks} ш")
        print(f"Цагдаа таниас {km_traveled - police_traveled} км-ийн зайтай байна")
        print(f"Тэмээний ядарсан хэмжээ: {camel_tired}%")
        print(f"Ам цангасан хэмжээ: {thirst}")
        print(f"Тэмээний нөхцөл байдал: {camel_condition}%")

    elif choice == "D":
        camel_tired = 0
        camel_condition = 100  # Тэмээ амрах үед эрч хүч нь сэргэнэ
        police_move = random.randint(6, 15)
        police_traveled += police_move
        print(f"Тэмээ амарч авлаа! Гэвч цагдаа {police_move} км зам тууллаа")

    elif choice == "C":
        if camel_condition <= 30:
            print("Тэмээ маш ядарсан байна. Энэ хурдтай явах нь аюултай байж магадгүй.")
        distance = random.randint(10, 20)
        km_traveled += distance
        thirst += 1
        camel_tired += random.choice([20, 30])
        police_traveled += random.randint(6, 15)
        print(f"Та {distance} км замыг бүх хурдаараа тууллаа")

        # Нууц зүйл тохиолдож магадгүй
        if not hidden_event and random.randint(1, 20) == 1:
            hidden_event = True
            print("""  
Таны замд тааралдсан нэгэн үл мэдэгдэх объект таны анхаарлыг татлаа.
Та үүнийг хурааж авсан бөгөөд хожим ашиглах боломжтой боллоо.
""")

        if random.randint(1, 20) == 1:
            thirst = 0
            camel_tired = 0
            drinks = 5
            print("""
Баянбүрд тааралдлаа баяр хүргэе!
Таны амны цангаа тайлагдаж савнуудаа усаар дүүргэж авлаа
Мөн таны тэмээ амарч авлаа
""")

    elif choice == "B":
        if camel_condition <= 50:
            print("Тэмээний биеийн байдал муу байна. Та удаан явбал асуудал үүсч мэднэ.")
        distance = random.randint(5, 12)
        km_traveled += distance
        thirst += 1
        camel_tired += random.choice([10, 20])
        police_traveled += random.randint(6, 15)
        print(f"Та {distance} км замыг дундаж хурдаар тууллаа")

        if random.randint(1, 20) == 1:
            thirst = 0
            camel_tired = 0
            drinks = 5
            print("""
Баянбүрд тааралдлаа баяр хүргэе!
Таны амны цангаа тайлагдаж савнуудаа усаар дүүргэж авлаа
Мөн таны тэмээ амарч авлаа
""")

    elif choice == "A":
        if drinks > 0:
            drinks -= 1
            thirst = 0
            print(f"Та ус уулаа. Үлдсэн ус: {drinks} ш")
        else:
            print("Ус дууссан!")

    # Цангах үед
    if thirst >= 5:
        print("Та цангаж үхлээ!")
        done = True
    elif thirst == 4:
        print("Та цангаж үхэх гэж байна!")
    elif thirst == 3:
        print("Та маш их цангасан байна!")

    # Тэмээ ядарсан үед
    if camel_tired >= 100:
        print("Таны тэмээ ядарч үхлээ!")
        done = True
    elif camel_tired > 50:
        print("Таны тэмээ маш их ядарсан байна!")

    # Цагдаа ойртож байгаа үед
    if police_traveled >= km_traveled:
        print("Цагдаа таныг барилаа!")
        done = True
    elif km_traveled - police_traveled <= 15:
        print("Цагдаа ойртож байна!")

    # Амжилттай зугтсан үед
    if km_traveled >= 200:
        print("Та чадлаа, их элсэн говийг амжилттай туулж цагдаагаас зугтаж чадлаа!")
        done = True
