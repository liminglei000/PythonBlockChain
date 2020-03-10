# demo:the times of sub_string queried from string based on KMP

def fail(sub_string):
    ans = [0] * (len(sub_string) + 1)
    for i in range(1, len(sub_string)):
        j = ans[i]
        while j > 0 and sub_string[i] != sub_string[j]:
            j = ans[j]
        if sub_string[i] == sub_string[j]:
            ans[i + 1] = j + 1
        else:
            ans[i + 1] = 0
    return ans
 
def count_substring(string, sub_string):
    next = fail(sub_string)
    cnt = 0
    start = 0
    length = len(string) - len(sub_string)
    i = 0
    while i <= length:
        while start < len(sub_string) and string[i + start] == sub_string[start]:
            start = start + 1
        if start == len(sub_string):
            cnt = cnt + 1
        i = i + start - next[start]
        if next[start] == 0:
            i = i + 1
        start = next[start]
    return cnt
 
if __name__ == "__main__":
    string = input().strip()
    sub_string = input().strip()
    count = count_substring(string, sub_string)
    print(count)
