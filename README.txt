fork from https://github.com/abhisg/nslookup
found error when run in armv4 & armv5
so, fix bug struct's bytes alignment
```c
// error: sizeof( struct R_DATA ) == 12 when on armv4 & armv5
#pragma pack(push, 1)
struct R_DATA /*RESOURCE RECORD DATA*/ {
    uint16_t type;
    uint16_t _class;
    uint32_t ttl;
    uint16_t data_len;
};
#pragma pack(pop)
```
** the correct code as below:**
```c
#pragma pack(push, 1)
struct R_DATA /*RESOURCE RECORD DATA*/ {
    uint16_t type;
    uint16_t _class;
    uint32_t ttl;
    uint16_t data_len;
}__attribute__((packed));
#pragma pack(pop)
```
>
> 1.Run the Makefile
>
> 2.Run the executable lookup as ./lookup <HOST NAME/IP>

