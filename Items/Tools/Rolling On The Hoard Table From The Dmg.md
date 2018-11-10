**Rolling on the Hoard Table from the DMG**  
*By Croebh#5603 and silverbass#2407*  
  
Use with `!hoard [cr]` (force a result with `!hoard [cr] [roll]`  
  
```  
!alias hoard embed {{cr,r,g,t=max(0,int("&1&")) if "&1&".isdigit() else 1,vroll(('1d100' if '&2&'=='&2'+'&' else '&2&')),load_json(get_gvar('2c232804-aac9-4195-a5d9-d35f7315f6c4')),0}}{{b=0 if cr in range(5) else 1 if cr in range(5,11) else 2 if cr in range(11,17) else 3}} -footer "{{g['footer']}}" {{g,G=g['hoard'],g['magicItems']}}
-title "Hoard Table for CR {{cr}} ({{'0-4' if b==0 else '5-10' if b==1 else '11-16' if b==2 else '17+'}}) - {{r.dice}}"
{{c={i:vroll(g[5][b][i]) for i in g[5][b] if g[5][b][i]} }}
-f "Currency|{{'\n'.join([f"{c[i].dice} = `{c[i].total:,} {i.upper()}`" for i in c])}}
{{k=[set('t',t+(c[x].total*(0.01 if x=='cp' else 0.1 if x=='sp' else 0.5 if x=='ep' else 10 if x=='pp' else 1))) for x in c]}}Total = `{{f"{round(t,2):,}"}} GP`"
{{B=g[b][[g[b].index(i) for i in g[b] if int(i[0])<=r.total<int(i[1])][0]]}}
{{N=[f"-f '{g[4][x]}|{vroll(B[x])}'" for x in range(2,13) if B[x]]}}{{''.join(N)}}
{{M={g[4][x]:vroll(B[x]) for x in range(13,22) if B[x]} }}

{{O='\n'}}
{{MM={z:[("" if set("v",vroll("1d100")) else "")+f"1d100 = `{str(v.total):0>2}` - "+"".join([m.name if m.min<=v.total<m.max else "" for m in G[z[-1]]]) for i in range(1,M[z].total+1)] for z in M} }}
{{'\n'.join([f" -f '{z}|{'**Number of Rolls:** '+str(M[z])+O if M[z].total>1 else ''}{O.join(MM[z])}'" for z in MM])}}
```  