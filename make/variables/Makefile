##:= vs =

	colon_rval := a

	#without colon, variable expands here as in c:

	colon := $(colon_rval)

	#without the colon, expansion takes the value of $(a) at the time of usage:

	nocolon = $(colon_rval)
	colon_rval := b

	#summary: always use colon unless you have a very good reason not to do so,
	#non colon equals is confusing!

	##eval and =

		#lazy eval also works with eval built-in

		nocolon_eval_rvar := a
		nocolon_eval = $(nocolon_eval_rvar)

##+=

	#evaluates immediately like `:=` if lvar was first defined with `:=`
	#and later if it was first defined with `=` or `?=`

	colon_plus_rval := c

	colon_plus := a
	colon_plus += b
	colon_plus += $(colon_plus_rval)

	nocolon_plus = a
	nocolon_plus += b
	nocolon_plus += $(colon_plus_rval)

	colon_plus_rval := d

##?=

	#Define variable only if it is not defined.

	question_var := a
	question_var ?= b

	#Empty variables are still defined.

	#Evaluation is defferred like in `=` (unlike `:=`)

	question_rval_defer := a
	question_var_defer ?= $(question_rval_defer)
	question_rval_defer := b

##$$

	#you can also use shell vars here:

	shell_var = $$a

##where variables can be used

	#you can use variables:

	#- to give other variable names
	#- to define rules
	#- to define recipes

	#name a variable with another variable:

	varname := avarname
	$(varname) := avarname_val

	varname2 := varname

	#TODO why does this not work:

	#vardef := vardef_name := vardef_val
	#$(vardef)

	#write a rule with a variable:

	rule := varrule: all

##multiline variable

	#create a multiline variable

	#TODO why does it not work? I copied from the manual!

	multiline_inner := multiline_2

define multiline =
@echo multiline_1
@echo $(multiline_inner)
endef

##automatic variables

	#variables that are automatically set, either at startup of MAKE or inside of rules
	#depending on the rule such as $@ or $?

	#some automatic variables can be defined in makefiles and have an effect

	##MAKE

		#TODO

	###MAKECMDGOALS

		#contains all targets given at commandline invocation

		#the default target if any does not count

	##MAKEFLAGS

		#flags given at invocation

	##MAKELEVEL

		#recursion level of make (how many makes called other makes)

		#starts at 0

	##SHELL

		#interpreter used to read each line

	##SUFFIXES

		#list of suffixes for which make automatically defines rules

	##VPATH

		#directories where to look for prerequisite files not found in current dir

.PHONY: all sh makecmdgoals

all:
	@#here you see how variables can be used inside recipes:
	@if [ ! "$(colon)" 				= "a"				]; then exit 1; fi
	@if [ ! "$(nocolon)" 			= "b" 				]; then exit 1; fi
	$(eval nocolon_eval_rvar := b)
	@if [ ! "$(nocolon_eval)" 		= "b" 				]; then exit 1; fi
	@if [ ! "$(colon_plus)"			= "a b c" 			]; then exit 1; fi
	@if [ ! "$(nocolon_plus)" 		= "a b d" 			]; then exit 1; fi
	@if [ ! "$(avarname)" 			= "avarname_val"	]; then exit 1; fi
	@if [ ! "$(question_var)"		= "a"				]; then exit 1; fi
	@if [ ! "$(question_var_defer)"	= "b"				]; then exit 1; fi
	@#you can use variables inside variables: varname2 -> avarname -> avarname:
	@if [ ! "$($(varname2))" 		= "avarname"		]; then exit 1; fi
	@#@if [ ! "$(multiline)" 			= $$'1\n2'			]; then exit 1; fi
	@#@if [ ! "$(vardef_name)"		= "vardef_val"		]; then exit 1; fi
	@a="b" && if [ ! "$(shell_var)" = b ]; then exit 1; fi
	$(multiline)
	@echo "CURDIR       = $(CURDIR)"
	@echo "MAKE         = $(MAKE)"
	@echo "MAKECMDGOALS = $(MAKECMDGOALS)"
	@echo "MAKEFLAGS    = $(MAKEFLAGS)"
	@echo "MAKEFILES    = $(MAKEFILES)"
	@echo "MAKELEVEL    = $(MAKELEVEL)"
	@echo "SHELL        = $(SHELL)"
	@echo "SUFFIXES     = $(SUFFIXES)"
	@echo "VPATH        = $(VPATH)"

$(rule)
	@echo varrule

#by the way, you can also use built-ins anywhere just like variables
#Try this with `make sh`:
$(shell echo sh):
	@echo sh

makecmdgoals:
	@#
