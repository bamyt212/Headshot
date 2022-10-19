function BAMYT() end
function setvalue(address,flags,value) BAMYT('Modify address value(Address, value type, value to be modified)') local tt={} tt[1]={} tt[1].address=address tt[1].flags=flags tt[1].value=value gg.setValues(tt) end
function SearchWrite(Search, Write, Type)    gg.clearResults()    gg.setVisible(false)    gg.searchNumber(Search[1][1], Type)    local count = gg.getResultCount()    local result = gg.getResults(count)    gg.clearResults()    local data = {}     local base = Search[1][2]    if (count > 0) then        for i, v in ipairs(result) do            v.isUseful = true         end        for k=2, #Search do            local tmp = {}            local offset = Search[k][2] - base             local num = Search[k][1]                         for i, v in ipairs(result) do                tmp[#tmp+1] = {}                 tmp[#tmp].address = v.address + offset                  tmp[#tmp].flags = v.flags              end            tmp = gg.getValues(tmp)             for i, v in ipairs(tmp) do                if ( tostring(v.value) ~= tostring(num) ) then                    result[i].isUseful = false                 end            end        end        for i, v in ipairs(result) do            if (v.isUseful) then                data[#data+1] = v.address            end        end        if (#data > 0) then           local t = {}           local base = Search[1][2]           for i=1, #data do               for k, w in ipairs(Write) do                   offset = w[2] - base                   t[#t+1] = {}                   t[#t].address = data[i] + offset                   t[#t].flags = Type                   t[#t].value = w[1]                   if (w[3] == true) then                      local item = {}                       item[#item+1] = t[#t]                       item[#item].freeze = true                       gg.addListItems(item)                   end                                 end           end           gg.setValues(t)           gg.addListItems(t)        else            gg.toast("", false)            return false        end    else        gg.toast("Vs NF")        return false    end end
function split(szFullString, szSeparator) local nFindStartIndex = 1 local nSplitIndex = 1 local nSplitArray = {} while true do local nFindLastIndex = string.find(szFullString, szSeparator, nFindStartIndex) if not nFindLastIndex then nSplitArray[nSplitIndex] = string.sub(szFullString, nFindStartIndex, string.len(szFullString)) break end nSplitArray[nSplitIndex] = string.sub(szFullString, nFindStartIndex, nFindLastIndex - 1) nFindStartIndex = nFindLastIndex + string.len(szSeparator) nSplitIndex = nSplitIndex + 1 end return nSplitArray end function xgxc(szpy, qmxg) for x = 1, #(qmxg) do xgpy = szpy + qmxg[x]["offset"] xglx = qmxg[x]["type"] xgsz = qmxg[x]["value"] gg.setValues({[1] = {address = xgpy, flags = xglx, value = xgsz}}) xgsl = xgsl + 1 end end function xqmnb(qmnb) gg.clearResults() gg.setRanges(qmnb[1]["memory"]) gg.searchNumber(qmnb[3]["value"], qmnb[3]["type"]) if gg.getResultCount() == 0 then gg.toast(qmnb[2]["name"] .. "") else gg.refineNumber(qmnb[3]["value"], qmnb[3]["type"]) gg.refineNumber(qmnb[3]["value"], qmnb[3]["type"]) gg.refineNumber(qmnb[3]["value"], qmnb[3]["type"]) if gg.getResultCount() == 0 then gg.toast(qmnb[2]["name"] .. "") else sl = gg.getResults(999999) sz = gg.getResultCount() xgsl = 0 if sz > 999999 then sz = 999999 end for i = 1, sz do pdsz = true for v = 4, #(qmnb) do if pdsz == true then pysz = {} pysz[1] = {} pysz[1].address = sl[i].address + qmnb[v]["offset"] pysz[1].flags = qmnb[v]["type"] szpy = gg.getValues(pysz) pdpd = qmnb[v]["lv"] .. ";" .. szpy[1].value szpd = split(pdpd, ";") tzszpd = szpd[1] pyszpd = szpd[2] if tzszpd == pyszpd then pdjg = true pdsz = true else pdjg = false pdsz = false end end end if pdjg == true then szpy = sl[i].address xgxc(szpy, qmxg) xgjg = true end end if xgjg == true then gg.toast(qmnb[2]["name"] .. "" .. xgsl .. "") else gg.toast(qmnb[2]["name"] .. "") end end end end
function setvalue(address,flags,value) local tt={} tt[1]={} tt[1].address=address tt[1].flags=flags tt[1].value=value gg.setValues(tt) end
function BamYT(Nc,Type,Search,Write) gg.clearResults() gg.setRanges(Nc) gg.setVisible(false) gg.searchNumber(Search[1][1],Type) local count=gg.getResultCount() local result=gg.getResults(count) gg.clearResults() local data={} local base=Search[1][2] if(count>0)then for i,v in ipairs(result)do v.isUseful=true end for k=2,#Search do local tmp={} local offset=Search[k][2]-base local num=Search[k][1] for i,v in ipairs(result)do tmp[#tmp+1]={} tmp[#tmp].address=v.address+offset tmp[#tmp].flags=v.flags end tmp=gg.getValues(tmp) for i,v in ipairs(tmp)do if(tostring(v.value)~=tostring(num))then result[i].isUseful=false end end end for i,v in ipairs(result)do if(v.isUseful)then data[#data+1]=v.address end end if(#data>0)then gg.toast("\n"..#data.."") local t={} local base=Search[1][2] for i=1,#data do for k,w in ipairs(Write)do offset=w[2]-base t[#t+1]={} t[#t].address=data[i]+offset t[#t].flags=Type t[#t].value=w[1] if(w[3]==true)then local item={} item[#item+1]=t[#t] item[#item].freeze=true gg.addListItems(item) end end end gg.setValues(t) gg.sleep(400) gg.toast("\n"..Name..""..#t.."") else gg.toast("\n"..Name.."") return false end else gg.toast("\n"..Name.."") return false end end
function RD(Search,Get,Type,Range,Name) gg.clearResults() gg.setRanges(Range) gg.setVisible(false) if Search[1][1]~=false then gg.searchAddress(Search[1][1],0xFFFFFFFF,Search[1][4] or Type,gg.SIGN_EQUAL,Search[1][5] or 1,Search[1][6] or -1) end gg.searchNumber(Search[1][2],Search[1][4] or Type,false,gg.SIGN_EQUAL,Search[1][5] or 1,Search[1][6] or -1) local count=gg.getResultCount() local result=gg.getResults(count) gg.clearResults() local data={} local base=Search[1][3] if (count > 0) then for i,v in ipairs(result) do v.isUseful=true end for k=2,#Search do local tmp={} local offset=Search[k][2] - base local num=Search[k][1] for i,v in ipairs(result) do tmp[#tmp+1]={} tmp[#tmp].address=v.address+offset tmp[#tmp].flags=Search[k][3] or Type end tmp=gg.getValues(tmp) for i,v in ipairs(tmp) do if v.flags==16 or v.flags==64 then values=tostring(v.value):sub(1,6) num=tostring(num):sub(1,6) else values=v.value end if tostring(values)~=tostring(num) then result[i].isUseful=false end end end for i,v in ipairs(result) do if (v.isUseful) then data[#data+1]=v.address end end if (#data > 0) then local t,t_={},{} local base=Search[1][3] for i=1,#data do for k,w in ipairs(Get) do offset=w[2] - base if w[1]==false then t_[#t_+1]={} t_[#t_].address=data[i]+offset t_[#t_].flags=Type th_=(th_) and th_+1 or 1 else t[#t+1]={} t[#t].address=data[i]+offset t[#t].flags=w[3] or Type t[#t].value=w[1] tg_=(tg_) and tg_+1 or 1 if (w[4]==true) then local item={} item[#item+1]=t[#t] item[#item].freeze=w[4] gg.addListItems(item) end end end end tg=(tg_) and "\n"..tg_.."" or "" th=(th_) and "" or "" gg.setValues(t) t_=gg.getValues(t_) gg.loadResults(t_) gg.toast("\n"..Name..tg) tg_,th_=nil,nil else gg.toast("",false) return false end else gg.toast("evil monk") return false end end
function readWrite(Search,Get,Type,Range,Name) gg["clearResults"]() gg["setRanges"](Range) gg["setVisible"](false) if Search[1][1]~=false then _G["gg"]["searchAddress"](Search[1][1],0xFFFFFFFF,Search[1][4] or Type,_G["gg"]["SIGN_EQUAL"],Search[1][5] or 1,Search[1][6] or -1) end gg["searchNumber"](Search[1][2],Search[1][4] or Type,false,_G["gg"]["SIGN_EQUAL"],Search[1][5] or 1,Search[1][6] or -1) local count=gg["getResultCount"]() local result=gg["getResults"](count) gg["clearResults"]() local data={} local base=Search[1][3] if (count > 0) then for i,v in ipairs(result) do v.isUseful=true end for k=2,#Search do local tmp={} local offset=Search[k][2] - base local num=Search[k][1] for i,v in ipairs(result) do tmp[#tmp+1]={} tmp[#tmp].address=v.address+offset tmp[#tmp].flags=Search[k][3] or Type end tmp=gg["getValues"](tmp) for i,v in ipairs(tmp) do if v.flags==16 or v.flags==64 then values=tostring(v.value):sub(1,6) num=tostring(num):sub(1,6) else values=v.value end if tostring(values)~=tostring(num) then result[i].isUseful=false end end end for i,v in ipairs(result) do if (v.isUseful) then data[#data+1]=v.address end end if (#data > 0) then local t,t_={},{} local base=Search[1][3] for i=1,#data do for k,w in ipairs(Get) do offset=w[2] - base if w[1]==false then t_[#t_+1]={} t_[#t_].address=data[i]+offset t_[#t_].flags=Type th_=(th_) and th_+1 or 1 else t[#t+1]={} t[#t].address=data[i]+offset t[#t].flags=w[3] or Type t[#t].value=w[1] tg_=(tg_) and tg_+1 or 1 if (w[4]==true) then local item={} item[#item+1]=t[#t] item[#item].freeze=w[4] gg["addListItems"](item) end end end end tg=(tg_) and "\n modify"..tg_.."data" or "" th=(th_) and "" or "" gg["setValues"](t) t_=gg["getValues"](t_) gg["loadResults"](t_) gg["toast"]("\n"..Name..tg) tg_,th_=nil,nil else gg["toast"]("Not searchable",false) return false end else gg["toast"]("Not searchable") return false end end
function edit(orig,ret)_om=orig[1].memory or orig[1][1]_ov=orig[3].value or orig[3][1]_on=orig[2].name or orig[2][1]gg.clearResults()gg.setRanges(_om)gg.searchNumber(_ov,orig[3].type or orig[3][2])sz=gg.getResultCount()if sz<1 then gg.toast(_on.."\nFailed to Open")else sl=gg.getResults(99999)for i=1,sz do ist=true for v=4,#orig do if ist==true and sl[i].value==_ov then cd={{}}cd[1].address=sl[i].address+(orig[v].offset or orig[v][2])cd[1].flags=orig[v].type or orig[v][3]szpy=gg.getValues(cd)cdlv=orig[v].lv or orig[v][1]cdv=szpy[1].value if cdlv==cdv then pdjg=true ist=true else pdjg=false ist=false end end end if pdjg==true then szpy=sl[i].address for x=1,#(ret)do xgpy=szpy+(ret[x].offset or ret[x][2])xglx=ret[x].type or ret[x][3]xgsz=ret[x].value or ret[x][1]xgdj=ret[x].freeze or ret[x][4]xgsj={{address=xgpy,flags=xglx,value=xgsz}}if xgdj==true then xgsj[1].freeze=xgdj gg.addListItems(xgsj)else gg.setValues(xgsj)end end xgjg=true end end if xgjg==true then gg.toast(_on.."\nSuccessfully Opened")else gg.toast(_on.."\nSuccessfully Opened")end end end
if true then 
local org = gg.searchNumber 
local hook = function(...) 
gg.setVisible(false) 
local ret = org(...) 
if gg.isVisible()then 
while true do os.exit() end 
end 
return ret 
end 
gg.searchNumber = hook 
end
gg.alert("INDONESIA\nJangan Buka Gg Saat Menjalankan Script/Bypass \n\nENGLISH\nDon't Open Gg While Running Script/Bypass \n\n\nWELCOME NEW SEASSON 16")
gg.setVisible(true)
gg.setVisible(true)
LuaLibrary = -1
function HOME()
MENU = gg.multiChoice({
        "Bypass Lobby",
        "Less Recoill",
        "Small Croshair",
        "Aimbot",
        "Auto Headshot",
        "Ipad View",
        "Night Mode",
        "No Fog",
        "EXIT" 
  }, nil, "64 BIT ONLY ") if MENU == nil then
  else
   if MENU[1] == true then 
      BAM1()
     end
   if MENU[2] == true then 
      BAM2()
     end
   if MENU[3] == true then 
      BAM3()
     end
   if MENU[4] == true then 
      BAM4()
     end
   if MENU[5] == true then 
      BAM5()
     end
  if MENU[6] == true then 
      BAM6()
     end
   if MENU[7] == true then 
      BAM7()
     end
   if MENU[8] == true then 
      BAM8()
     end
   if MENU[9] == true then
      LOBBY()
     end
   end
  LuaLibraryTool = -1
end

function BAM1() 
gg.alert("Mulai?")
gg.clearResults()
gg.setRanges(gg.REGION_C_ALLOC)
gg.searchNumber("196,864;16,842,753::5", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1) 
if gg.getResultCount() == 0 then
gg.alert("RESTART AGAIN")
  gg.processKill()
os.exit()
else
gg.searchNumber("196,864", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
n = gg.getResultCount()
jz = gg.getResults(n)
for i = 1, n do
end
end
gg.clearResults()
gg.setVisible(false)
gg.setRanges(gg.REGION_C_ALLOC)
gg.searchNumber("144,387;133634", 4)
gg.setVisible(false)
gg.refineNumber("144,387", 4)
gg.setVisible(false)
gg.getResults(99931)
gg.editAll("84,149,249", 4)
gg.clearResults()
gg.setRanges(gg.REGION_C_ALLOC)
gg.setVisible(false)
gg.searchNumber("134,658;134,658", 4)
gg.setVisible(false)
gg.refineNumber("134,658", 4)
gg.getResults(99931)
gg.setVisible(false)
gg.editAll("84,149,249", 4)
gg.clearResults()
gg.setRanges(gg.REGION_C_ALLOC)
gg.setVisible(false)
gg.searchNumber("134,914;262,403", 4)
gg.setVisible(false)
gg.refineNumber("134,914", 4)
gg.getResults(99931)
gg.setVisible(false)
gg.editAll("84,149,249", 4)
gg.clearResults()
gg.setRanges(gg.REGION_C_ALLOC)
gg.setVisible(false)
gg.searchNumber("133,378;133,634", 4)
gg.getResults(99931)
gg.setVisible(false)
gg.editAll("84,149,249", 4)
gg.clearResults()
gg.setRanges(gg.REGION_C_ALLOC)
gg.setVisible(false)
gg.searchNumber("196,864;16,842,753", 4)
gg.setVisible(false)
gg.refineNumber("196,864", 4)
gg.getResults(99931)
gg.setVisible(false)
gg.editAll("84,149,249", 4)
gg.clearResults()
end

function BAM2() 
so=gg.getRangesList('libUE4.so')[1].start
py=0x1A2B058 
setvalue(so+py,4,505425152)--less recoill
end

function BAM3() 
so=gg.getRangesList('libUE4.so')[1].start
py=0x1A2C54C 
setvalue(so+py,4,505425152)--small
end

function BAM4() 
so=gg.getRangesList('libUE4.so')[1].start
py=0x2670848
setvalue(so+py,16,8.476953379792e-21)
so=gg.getRangesList('libUE4.so')[1].start
py=0x2670844 
setvalue(so+py,4,505421832)--aimbot
so=gg.getRangesList('libUE4.so')[1].start
py=0x2670754 
setvalue(so+py,4,505421832 )
so=gg.getRangesList('libUE4.so')[1].start
py=0x26707B4 
setvalue(so+py,4,505421832 )
so=gg.getRangesList('libUE4.so')[1].start
py=0x26707FC 
setvalue(so+py,4,505421832 )
so=gg.getRangesList('libUE4.so')[1].start
py=0x2F1C74C 
setvalue(so+py,4,505421832 )
end

function BAM5() 
gg.clearResults()
gg.setRanges(gg.REGION_ANONYMOUS)
gg.setVisible(false)
gg.searchNumber("25;30.5", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.setVisible(false)
gg.refineNumber("25;30.5", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(10)
gg.setVisible(false)
gg.editAll("500", gg.TYPE_FLOAT)
gg.clearResults()
end

function BAM6() 
so=gg.getRangesList('libUE4.so')[1].start
py=0x4B54E7C 
setvalue(so+py,16,1.2)--Ipad View
end

function BAM7() 
so=gg.getRangesList('libUE4.so')[1].start
py=0x2E445A4 
setvalue(so+py,16,8.47695338e-21 )--night mode
end

function BAM8() 
so=gg.getRangesList('libUE4.so')[1].start
py=0x2E2ABC4 
setvalue(so+py,4,706675684)--No Fog
end


function LOBBY() 
os.date("%G-%m-%d | TIME: %H:%M:%S") 
print("ANDA BANED KAMI SENANG")
gg.skipRestoreState()
  gg.setVisible(true)
  os.exit()
end
while true do
  Time = os.date("%G-%m-%d | TIME: %H:%M:%S")
  if gg.isVisible(true) then
    LuaLibraryTool = 1
    gg.setVisible(false)
  end
  if LuaLibraryTool == 1 then
    HOME()
  end
end
