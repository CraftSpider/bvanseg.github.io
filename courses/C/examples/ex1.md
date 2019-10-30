```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <stdbool.h>


char* make_str(char c) {
    char* out = malloc(sizeof(char) * 2);
    out[0] = c;
    out[1] = '\0';
    return out;
}


char* concat_str(const char* str, const char* str2) {
    ssize_t len = strlen(str) + strlen(str2);
    char* output = malloc(sizeof(char) * len);
    strcat(output, str);
    strcat(output, str2);
    return output;
}


char* concat_char(char* str, char c) {
    char* temp = make_str(c);
    char* out = concat_str(str, temp);
    free(temp);
    free(str);
    return out;
}


char* new_str() {
    char* out = malloc(1);
    out[0] = '\0';
    return out;
}


void scanfp(const char* format, void* in) {
    ssize_t length = strlen(format);
    bool in_format = false;
    char* cur_form = new_str();
    
    for (ssize_t i = 0; i < length; ++i) {
        char c = format[i];
        char* s = make_str(c);
        
        if (in_format) {
            cur_form = concat_char(cur_form, c);
            if (strstr("iduoxfegacsp]n", s)) {
                scanf(cur_form, in);
                in += sizeof(int32_t);
                in_format = false;
                cur_form = new_str();
            }
        } else {
            if (c == '%') {
                in_format = true;
            }
            cur_form = concat_char(cur_form, c);
        }
        
        free(s);
    }
}

int main() {
    int* intarr = malloc(sizeof(int) * 3);
    scanfp("%d-%f-%d", intarr);
    printf("%d-%f-%d", intarr[0], ((float*)intarr)[1], intarr[2]);
    return 0;
}
```