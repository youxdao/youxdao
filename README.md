# NotePad

This is an AndroidStudio rebuild of google SDK sample NotePad

##拓展功能
本项目对NotePad进行了三个功能拓展，如下：\<br>
###1NoteList中显示条目增加时间显示
###2笔记查询（按标题查询）
###3笔记排序(按创建时间或修改时间)
##拓展功能解析
###1NoteList中显示条目增加时间显示
在NotePad原应用中，笔记列表只显示了笔记的标题。首先，找到列表中item的布局：noteslist_item.xml。要在标题下方加时间显示，就要在标题的TextView下再加一个时间的TextView。
但是由于原应用列表item只需要一个标题，所以不需要用上别的布局，而我要多加一个时间TextView，就要把标题TextView和时间TextView放入垂直的线性布局\<br>
NotePad原应用已经保存了时间，但是，这并不是我们平常所见到的时间格式，而是时间戳，需要对这些数据进行转化，使人能看的懂。
我选择的方法时把时间戳改为以时间格式存入，改动地方分别为NotePadProvider中的insert方法和NoteEditor中的updateNote方法。\<br>

###2笔记查询（按标题查询）
要添加笔记查询功能，就要在应用中增加一个搜索的入口。找到菜单的xml文件，list_options_menu.xml，添加一个搜索的item，搜索图标用安卓自带的图标.\<br>
在case语句中写跳转activity代码之前要先写好搜索的activity，新建一个名为NoteSearch的activity。由于搜索出来的也是笔记列表，所以可以模仿NoteList的activity继承ListActivity。.\<br>
要动态地显示搜索结果，就要对SearchView文本变化设置监听.动态搜索的实现最主要的部分在onQueryTextChange方法中，而onQueryTextChange方法作用是，当SearchView中文本发生变化时，执行其中代码，\<br>
搜索还有一个重要的部分就是要做到模糊匹配而不是严格匹配，可以使用数据库查询语句中的LIKE和%结合来实现，newText为输入搜索的内容：String[] selectionArgs = { "%"+newText+"%" };\<br>
最后要在AndroidManifest.xml注册NoteSearch：\<br>

###3笔记排序(按创建时间或修改时间)
笔记排序相对来说简单，只要把Cursor的排序参数变换下就可以了。并且在NoteList菜单switch下添加case：\<br>

