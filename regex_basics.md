# REGEX 기본 검색
# re.search()는 문자열 안에서 패턴을 찾음

import re

# "plaza" 안에 "aza"가 있는지 검색
result = re.search(r"aza", "plaza")
print(result)

# Output:
# <re.Match object; span=(2, 5), match='aza'>

# span=(2, 5)
# → 2번째 위치부터 5번째 전까지 match
# → 즉 "aza"를 찾았다는 의미


# --------------------------------------------------


# "maze" 안에 "aza"가 있는지 검색
result = re.search(r"aza", "maze")
print(result)

# Output:
# None

# "maze" 안에는 "aza" 패턴이 없어서
# 아무것도 찾지 못함


# --------------------------------------------------


# ^ = 문자열의 시작(start)을 의미함
# 문자열이 x로 시작하는지 검사

print(re.search(r"^x", "xenon"))

# Output:
# <re.Match object; span=(0, 1), match='x'>

# "xenon"은 x로 시작하므로 match됨


# --------------------------------------------------


# . = 아무 문자 하나(any single character)

print(re.search(r"p.ng", "penguin"))

# Output:
# <re.Match object; span=(0, 4), match='peng'>

# p + 아무 문자 하나 + ng 형태를 찾음
# "peng"가 조건에 맞아서 match됨

# REGEX 문자 그룹 / 범위 / 제외 / OR
# [] 는 여러 문자 중 하나를 의미함

# --------------------------------------------------
# 1. [Pp] = P 또는 p
# "Python" 또는 "python" 둘 다 찾을 수 있음

print(re.search(r"[Pp]ython", "Python"))

# Output:
# <re.Match object; span=(0, 6), match='Python'>


# --------------------------------------------------
# 2. [a-z] = 소문자 a부터 z 중 하나

print(re.search(r"[a-z]way", "The end of the highway"))

# 의미:
# 소문자 하나 + way 형태를 찾음
# highway 안의 "hway"가 조건에 맞음

# Output:
# <re.Match object; span=(15, 19), match='hway'>


# --------------------------------------------------
# 3. [a-zA-Z0-9] = 영문자 또는 숫자 하나

print(re.search(r"cloud[a-zA-Z0-9]", "cloudy"))
print(re.search(r"cloud[a-zA-Z0-9]", "cloud9"))

# 의미:
# cloud 뒤에 영문자 또는 숫자가 오는지 찾음
# cloudy → cloud + y
# cloud9 → cloud + 9


# --------------------------------------------------
# 4. [^a-zA-Z] = 영문자가 아닌 문자 하나
# [] 안에서 ^ 는 "제외"를 의미함

print(re.search(r"[^a-zA-Z]", "This is a sentence with spaces."))

# 의미:
# 영문자가 아닌 첫 번째 문자를 찾음
# 여기서는 단어 사이의 공백이 먼저 match됨


# --------------------------------------------------
# 5. [^a-zA-Z ] = 영문자도 아니고 공백도 아닌 문자 하나

print(re.search(r"[^a-zA-Z ]", "This is a sentence with spaces."))

# 의미:
# 알파벳도 아니고 공백도 아닌 문자를 찾음
# 여기서는 마지막 마침표 "."가 match됨


# --------------------------------------------------
# 6. cat|dog = cat 또는 dog
# | 는 OR 의미

print(re.search(r"cat|dog", "I like cats."))
print(re.search(r"cat|dog", "I love dogs!"))

# 의미:
# cat 또는 dog 중 먼저 발견되는 것을 찾음


# --------------------------------------------------
# 7. findall() = 조건에 맞는 모든 결과 찾기

print(re.findall(r"cat|dog", "I like both dogs and cats."))

# Output:
# ['dog', 'cat']

# search()는 첫 번째 match만 찾고
# findall()은 match되는 모든 결과를 리스트로 반환함

# REGEX 수량 표현
# *, +, ? 는 문자가 몇 번 나오는지 표현할 때 사용함


# --------------------------------------------------
# 8. .* = 아무 문자 0개 이상
# * 는 "0개 이상 반복" 의미

print(re.search(r"Py.*n", "Pygmalion"))

# 의미:
# Py로 시작하고 중간에 아무 글자들이 오다가
# 마지막에 n이 오는 패턴 찾기

# Output:
# <re.Match object; match='Pygmalion'>


print(re.search(r"Py.*n", "Python Programming"))

# "Python Programmin" 까지 match됨
# .* 가 가능한 많이 포함하려고 하기 때문


# --------------------------------------------------
# 9. [a-z]* = 소문자 0개 이상

print(re.search(r"Py[a-z]*n", "Python Programming"))

# 의미:
# Py 다음에 소문자가 여러 개 나오고
# 마지막이 n인 패턴 찾기

# "Python" match


print(re.search(r"Py[a-z]*n", "Pyn"))

# Output:
# <re.Match object; match='Pyn'>

# 소문자가 0개여도 가능
# * 는 0개 이상 허용


# --------------------------------------------------
# 10. + = 1개 이상 반복

print(re.search(r"o+l+", "goldfish"))

# 의미:
# o가 1개 이상 나오고
# 그 뒤에 L이 1개 이상 나오는 패턴 찾기

# Output:
# match='ol'

# o 1개 + L 1개 형태


print(re.search(r"o+l+", "woolly"))

# Output:
# <re.Match object; match='ooll'>

# oo + ll 형태라서 match


print(re.search(r"o+l+", "boil"))

# Output:
# None

# o 다음에 i가 와서 조건 불만족


# --------------------------------------------------
# 11. ? = 있어도 되고 없어도 됨
# 앞 문자가 0개 또는 1개

print(re.search(r"p?each", "To each their own"))

# Output:
# <re.Match object; match='each'>

# p가 없어도 match 가능


print(re.search(r"p?each", "I like peaches"))

# Output:
# <re.Match object; match='peach'>

# p가 있어도 match 가능

# REGEX 특수문자와 문자 클래스
# \ 는 특수문자를 문자 그대로 사용할 때 사용함


# --------------------------------------------------
# 12. . = 아무 문자 하나

print(re.search(r".com", "welcome"))

# Output:
# <re.Match object; match='lcom'>

# . 은 아무 문자 하나를 의미함
# 그래서 l + com 형태인 "lcom" 이 match됨


# --------------------------------------------------
# 13. \. = 마침표(.) 자체를 의미함

print(re.search(r"\.com", "welcome"))

# Output:
# None

# welcome 안에는 ".com" 이 없음


print(re.search(r"\.com", "mydomain.com"))

# Output:
# <re.Match object; match='.com'>

# \. 은 실제 마침표를 찾음
# 따라서 ".com" 이 match됨


# --------------------------------------------------
# 14. \w = 문자, 숫자, 언더바(_)
# * = 0개 이상 반복

print(re.search(r"\w*", "This is an example"))

# Output:
# <re.Match object; match='This'>

# \w 는:
# 문자, 숫자, _ 만 포함

# 공백(space)은 포함되지 않기 때문에
# "This" 까지만 match됨


print(re.search(r"\w*", "And_this_is_another"))

# Output:
# <re.Match object; match='And_this_is_another'>

# _ 도 \w 에 포함되므로
# 전체 문자열이 match됨

# REGEX 문자열 시작/끝 검사와 변수명 패턴


# --------------------------------------------------
# 15. .* = 아무 문자 0개 이상
# ^ = 문자열 시작
# $ = 문자열 끝

print(re.search(r"A.*a", "Argentina"))

# Output:
# <re.Match object; span=(0, 9), match='Argentina'>

# A로 시작하고
# 중간에 아무 문자가 오다가
# 마지막에 a가 나오는 패턴


print(re.search(r"A.*a", "Azerbaijan"))

# Output:
# <re.Match object; span=(0, 9), match='Azerbaija'>

# Regex는 조건에 맞는 부분까지만 match
# 마지막 n은 포함되지 않음


print(re.search(r"^A.*a$", "Australia"))

# Output:
# <re.Match object; span=(0, 9), match='Australia'>

# ^ = 문자열 시작
# $ = 문자열 끝

# 즉:
# 문자열 전체가
# A로 시작하고 a로 끝나는지 검사


# --------------------------------------------------
# 16. 변수명(valid variable name) 검사 패턴

pattern = r"^[a-zA-Z_][a-zA-Z0-9_]*$"

# 패턴 의미:
#
# ^                    → 문자열 시작
#
# [a-zA-Z_]            → 첫 글자는
#                        영문자 또는 _ 만 가능
#
# [a-zA-Z0-9_]*        → 그 뒤에는
#                        영문자, 숫자, _ 가
#                        0개 이상 가능
#
# $                    → 문자열 끝


print(re.search(pattern, "_this_is_a_valid_variable_name"))

# Output:
# <re.Match object; span=(0, 30), match='_this_is_a_valid_variable_name'>

# 올바른 변수명
# _ 로 시작 가능


print(re.search(pattern, "this isn't a valid variable"))

# Output:
# None

# 공백(space)
# 작은따옴표(')
# 포함되어 있어서 invalid


print(re.search(pattern, "my_variable1"))

# Output:
# <re.Match object; span=(0, 12), match='my_variable1'>

# 영문자 + 숫자 + _ 조합 가능


print(re.search(pattern, "2my_variable1"))

# Output:
# None

# 숫자로 시작할 수 없음
