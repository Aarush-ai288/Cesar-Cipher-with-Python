# Cesar-Cipher-with-Python
This code shifts each character of inputted text by a desired amount of letters in the alphabet. For instance, if you input ("hello", 3), the function will return "khoor".


def cipher(char, num):
    val = char
    ascii_char = ord(char)
    ascii_char += num % 26
    if 91 <= ascii_char <= 96:
        ascii_char -= 26
    if val.isupper() and 97 <= ascii_char <= 122:
        ascii_char -= 26
    if val.islower() and ascii_char > 122:
        ascii_char -= 26
    if not val.isalpha():
        return char
    return chr(ascii_char)


def cipher_string(text, num):
    new_str = ""
    for i in range(len(text)):
        new_str += cipher(text[i], num)
    return new_str


test1 = cipher_string("T22e qu!ck br0wn f0x", -3)
print(test1)
test2 = cipher_string("Hello", -2600000)
for i in range(5):
    print(test2, end="! ")
print()


def checker():
    tests = [
        ("The quick brown fox", 26),
        ("The quick brown fox", -26),
        ("The quick brown fox", 2600),
        ("The quick brown fox", -2600),
        ("The quick brown fox", 3),
        ("The quick brown fox", -3),
        ("The qu!ck br0wn f0x", 3),
        ("The qu!ck br0wn f0x", -3),
        ("tHE QU!cK Br0WN f0X", 3),
        ("tHE QU!cK Br0WN f0X", -3),
    ]

    answers = ["The quick brown fox",
               "The quick brown fox",
               "The quick brown fox",
               "The quick brown fox",
               "Wkh txlfn eurzq ira",
               "Qeb nrfzh yoltk clu",
               "Wkh tx!fn eu0zq i0a",
               "Qeb nr!zh yo0tk c0u",
               "wKH TX!fN Eu0ZQ i0A",
               "qEB NR!zH Yo0TK c0U"
               ]

    correctList, wrongList = [], []
    ct, correct, wrong, = 0, 0, 0

    for i in range(len(tests)):
        textShift = tests[i]
        ans = answers[i]
        result = cipher_string(*textShift)

        print("{:30s}".format(str(textShift)), "--> ", result, end=" ")
        if ans == result:
            print("✓")
            correct += 1
            correctList.append(textShift)
        else:
            print("X")
            wrong += 1
            wrongList.append(textShift)
        ct += 1
    print("\n")
    print("Correct: " + str(correct) + "/" + str(len(answers)))
    if (wrongList != []):
        print("Incorrect:")
        for wrong in wrongList:
            print(" - " + str(wrong))


checker()
