Moon
===
* Verify the file type:
```
[littlewho@sweethome timctf]$ file moon
moon: Lua bytecode,
```
* Decompile lua:
```
[littlewho@sweethome timctf]$ unluac moon
local L0_0, L1_1, L2_2, L3_3, L4_4
L0_0 = require
L1_1 = "sha1"
L0_0 = L0_0(L1_1)
L1_1 = {
  L2_2,
  L3_3,
  L4_4,
  "cce7a2323221879a3e974e7203bb6ec68f8b50bd",
  "45c38bd60f7da9b278b89c358589ce828f06f49f",
  "766dd89c822789d0336b844d3bccde758e1f90e5",
  "b384aa81ae4523773a134b73455a9afddb229a5a",
  "ca94e97a10b8994175c9fd4a51d47f419c46ac61",
  "8fbe44e56aa7c0901570a8d009f7ccf0e348f431",
  "5a2253385821467f8f2589b53b211034abbeac85",
  "00c6bcab76d8f6c32b515d6799860fee7939ba6f",
  "dcbb8f39c4cfe9efad45201f7f267ac77a456702",
  "cdbc1e5fe6fa5613dbe63abd3d797f25684e471e",
  "68ad637b88e40d82fb861bfcd4e21ab82d7a834f",
  "645560680eb9f12c3e329cf9deb240cf79cb0647",
  "bd30e3a75020e800c309d6cc7a0dd0a571380e29",
  "bb64ae072018da59768ad26056a096c44f8f006b",
  "571725d2c6bc92151bdf44acd398651cbfc16313",
  "880641faa27d5771cbf210c24883ffc385f98b29",
  "ce06ec74f409c35beb9bb6b45f9c031865b980b6",
  "f4cd74a94cd4378e6ab9e39de94d16b5a2b6b522"
}
L2_2 = "f721abcc5553f0dda9206cfd090e1a414a3b6e85"
L3_3 = "f31cae2c5f41b31c956942a8a7e47ea2b9d1cb5a"
L4_4 = "6078aa809fd2431189f95c1676ff10047e8f9c86"
function L2_2(A0_5)
  local L1_6, L2_7, L3_8, L4_9, L5_10
  L1_6(L2_7, L3_8)
  for L4_9, L5_10 in L1_6(L2_7) do
    if string.reverse(L5_10) ~= L0_0(string.sub(A0_5, 1, L4_9)) then
      return false
    end
  end
  return L1_6
end
function L3_3(A0_11)
  local L1_12, L2_13, L3_14, L4_15
  L1_12 = [[
   There was, as in the fairy tales,
   As ne'er in the time's raid,
   There was, of famous royal blood
   A most beautiful maid.
]]
  L2_13 = [[
   She was her parents' only child,
   Bright like the sun at noon,
   And like the virgin midst the saints
   And among stars the moon.
]]
  L3_14 = [[
   From the deep shadow of the vaults
   Her step now she directs
   Toward a window: at its nook
   Bright Luciflag<%s> expects.

   ...
]]
  L4_15 = string
  L4_15 = L4_15.rep
  L4_15 = L4_15("*", 21)
  if A0_11 ~= nil and L2_2(A0_11) then
    L4_15 = A0_11
  end
  io.stdout:write(L1_12 .. "\n")
  io.stdout:write(L2_13 .. "\n")
  io.stdout:write(string.format(L3_14, L4_15))
end
function L4_4()
  io.stdout:write([[
	--=== TimCTF poetry club ===--

]])
  io.stdout:write([[
	:: Homework 1 | "Luciflag"  ::

]])
  L3_3(arg[1])
end
L4_4()
```
* Get some strings out of the executable:
```
[littlewho@sweethome timctf]$ strings moon
LuaS
require
sha1
)f721abcc5553f0dda9206cfd090e1a414a3b6e85
)f31cae2c5f41b31c956942a8a7e47ea2b9d1cb5a
)6078aa809fd2431189f95c1676ff10047e8f9c86
)cce7a2323221879a3e974e7203bb6ec68f8b50bd
)45c38bd60f7da9b278b89c358589ce828f06f49f
)766dd89c822789d0336b844d3bccde758e1f90e5
)b384aa81ae4523773a134b73455a9afddb229a5a
)ca94e97a10b8994175c9fd4a51d47f419c46ac61
)8fbe44e56aa7c0901570a8d009f7ccf0e348f431
)5a2253385821467f8f2589b53b211034abbeac85
)00c6bcab76d8f6c32b515d6799860fee7939ba6f
)dcbb8f39c4cfe9efad45201f7f267ac77a456702
)cdbc1e5fe6fa5613dbe63abd3d797f25684e471e
)68ad637b88e40d82fb861bfcd4e21ab82d7a834f
)645560680eb9f12c3e329cf9deb240cf79cb0647
)bd30e3a75020e800c309d6cc7a0dd0a571380e29
)bb64ae072018da59768ad26056a096c44f8f006b
)571725d2c6bc92151bdf44acd398651cbfc16313
)880641faa27d5771cbf210c24883ffc385f98b29
)ce06ec74f409c35beb9bb6b45f9c031865b980b6
)f4cd74a94cd4378e6ab9e39de94d16b5a2b6b522
assert
Argument is nil
ipairs
string
reverse
   There was, as in the fairy tales,
   As ne'er in the time's raid,
   There was, of famous royal blood
   A most beautiful maid.
   She was her parents' only child,
   Bright like the sun at noon,
   And like the virgin midst the saints
   And among stars the moon.
   From the deep shadow of the vaults
   Her step now she directs
   Toward a window: at its nook
   Bright Luciflag<%s> expects.
   ...
string
stdout
write
format
stdout
write
"	--=== TimCTF poetry club ===--
"	:: Homework 1 | "Luciflag"  ::
```
* We can see that there are few strings that looks like function names. After a little bit of analysis, we could observe that the most things happen in function L2_2, it takes arg[1] as its argument and returns true if the input is correct. If we colerate the found function names with the pseudo-code we got we get something more reliable:
```
array = [... hashes here ...]
for (i, k) in ipairs(array):
    if string.reverse(k) != sha1(string.sub(k, 1, i)):
        return false
retur true
```
* We observe that we could brute-force the correct input character by character:
```
 with open("hashes.txt") as f:
     hashes = [x.strip('\n ') for x in f.readlines()]
 
 from string import printable
 from hashlib import sha1
 
 flag = ""
 for (i, h) in  enumerate(hashes):
     for ch in printable:
         temp = flag + ch
         nh = sha1()
         nh.update(temp.encode('utf-8'))
         if h[::-1] == nh.hexdigest():
             flag = temp
print (flag)
```
* And the flag is: `et3rnal_c0ld_4nd_tru3`
