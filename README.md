# python
mypythonproject
if (currsection == lit.WORKING_STORAGE and 
    re.search(lit.regex_varmultilinedef,currline))
	lookfwdlines = 0
	vardefstmt = ''
	while re.search(lit.regex_term,cobolpgm[currlinepos+lookfwdlines]) is None:
		vardefstmt += cobolpgm[currlinepos+lookfwdlines].strip('\n')
		lookfwdlines += 1
	vardefstmt += cobolpgm[currlinepos+lookfwdlines].strip('\n')
	skiplines = lookfwdlines
	normalizedcobolpgm.append(vardefstmt)
	res = re.search(lit.regex_vardef,vardefstmt)
	if res:
		variables[res.group(2)] = {}
		variables[res.group(2)]['level'] = res.group(1)
		variables[res.group(2)]['pic'] = res.group(3)
		variables[res.group(2)]['record'] = currrecord
		variables[res.group(2)]['prefix1'] = res.group(2).split('-',1)[0]
		try:
			variables[res.group(2)]['prefix2'] = res.group(2).split('-',2)[0] + '-' + res.group(2).split('-',2)[1]
		except IndexError:
			variables[res.group(2)]['prefix2'] = ' '
	continue
	
if re.search(lit.regex_recordlevel, currline)
	currrecord = re.search(lit.regex_recordlevel, currline).group(1)
	continue
	
if currsection = lit.WORKING_STORAGE and 
   re.search(lit.regex_vardef,currline):
   res = re.search(lit.regex_vardef,currline)
   if res.group(2):
	  if 'FILLER' in res.group(2) :
	      normalizedcobolpgm.append(currline)
		  continue
	   else:
		variables[res.group(2)] = {}
		variables[res.group(2)]['level'] = res.group(1)
		variables[res.group(2)]['pic'] = res.group(3)
		variables[res.group(2)]['record'] = currrecord
		variables[res.group(2)]['prefix1'] = res.group(2).split('-',1)[0]
		try:
			variables[res.group(2)]['prefix2'] = res.group(2).split('-',2)[0] + '-' + res.group(2).split('-',2)[1]
		except IndexError:
			variables[res.group(2)]['prefix2'] = ' '
		    continue
    normalizedcobolpgm.append(currline)
    continue

if re.search(lit.regex_multimoveline, currline):
    currline+= cobolpgm[currlinepos+1]

if re.search(lit.regex_move,currline):
   movestmts.append(currline)
   res = re.search(lit.regex_move,currline)
   MoveFromVar = res.group(1)
   try:
      variables[res.group(2)]['MoveFrom'] = MoveFromVar
      if re.search(lit.regex_moveliteral,MoveFromVar):
         pass
      else:
         variables[res.group(1)]['MoveTo'] = res.group(2)
		 variables[res.group(20)]['MoveFromRec'] = variables[res.group(1)]['record']
	  normalizedcobolpgm.append(currline)
	  lookfwdlines = 1
	  while re.search(lit.regex_movecont,cobolpgm[currlinepos+lookfwdlines]):
	     res = re.search(lit.regex_movecont,cobolpgm[currlinepos+lookfwdlines])
		 variables[res.group(1)]['MoveFrom'] = MoveFromVar
		 if re.search(lit.regex_moveliteral,MoveFromVar) :
		    pass
	     else :
		    variables[res.group(1)]['MoveFromRec'] = variables[MoveFromVar]['record']
		 normalizedcobolpgm.append(cobolpgm[currlinepos+lookfwdlines])
		 movestmts.append(' MOVE '+ MoveFromVar + ' TO ' + cobolpgm[currlinepos+lookfwdlines].lstrip())
		 if re.search(lit.regex_term,cobolpgm[currlinepos+lookfwdlines])):
		    break
		 lookfwdlines+=1
	   skiplines = lookfwdlines - 1
	   continue
	except KeyError:
	
if re.search(lit.regex_conditions,currline):
    rulestmt = ''
	lookfwdlines= 0
	rulelevel = 1
	normalizedcobolpgm.append(currline)
	while re.search(lit.regex_scopeterm,cobolpgm[currlinepos+lookfwdlines]) and rulelevel > 0 :
	   normalizedcobolpgm.append(cobolpgm[currlinepos+lookfwdlines])
	   rulestmt+= cobolpgm[currlinepos+lookfwdlines]
	   if re.search(lit.regex_conditions,cobolpgm[currlinepos+lookfwdlines]):
	      rulelevel+= 1
	   if re.search(lit.regex_rulesscopeterm,cobolpgm[currlinepos+lookfwdlines]):
	      rulelevel-=1
	   lookfwdlines+=1
	rulelevel += cobolpgm[currlinepos+lookfwdlines]
	ruleswriter.writerow(rulestmt)
	skiplines = lookfwdlines
	continue

	   
if re.search(lit.regex_moveof, currline):
   movestmts.append(currline)
   res = re.search(lit.regex_moveof,currline)
   MoveFromVar = res.group(1)
   MoveToVar = res.group(2)
   MoveToRec = res.group(3)
   if re.search(lit.regex_moveliteral,MoveFromVar):
       variables[MoveToVar]['MoveFrom'] += MoveFromVar
   else:
       variables[MoveFromVar]['MoveTo'] = MoveToVar
	   variables[MoveFromVar]['MoveToRec'] = MoveToRec
	   variables[MoveToVar]['MoveFrom'] += MoveFromVar
	   variables[MoveToVar]['MoveFromRec'] += variables[MoveFromVar]['record']
    continue	   
	   
for k, v in variables.items():
   for rulestmt in rulestmts:
		if k in rulestmt:
			v['RuleAssociated'] = v.get('RuleAssociated',' ') + rulestmt
	for movestmt in movestmts:
		if k in movestmt:
			v['MoveAssociated'] = v.get('MoveAssociated',' ') + movestmt
   varswriter.writerow([k,v['level'],v['pic'],v['record']..)
   
   
