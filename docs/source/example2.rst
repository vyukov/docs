Script
======

скрипт, для поиска несоответствующих шейпов в аутлайнере (нужно выделить группые geo объектов), если при конекте анимации на сюрф модель произошли баги

.. code-block:: python
   

	import maya.cmds as cmds
	sel_lst=cmds.ls(sl=1)

	def diff_(grp_1=None,grp_2=None):
		cmds.select(grp_1, hi=1,r=1)
		elem_a =[ elem.replace('|'+grp_1,'') for elem in cmds.ls(sl=1,l=1) ]

		cmds.select(grp_2, hi=1,r=1)
		elem_b =[ elem.replace('|'+grp_2,'') for elem in cmds.ls(sl=1,l=1) ]

		cmds.select(cl=1)
		dif = ( set(elem_a)^set(elem_b) )     

		for cyc_var in dif:
			if cyc_var in elem_a:
				out = grp_1+cyc_var
			if cyc_var in elem_b:
				out = grp_2+cyc_var        

			print out       

	diff_(sel_lst[0],sel_lst[1])