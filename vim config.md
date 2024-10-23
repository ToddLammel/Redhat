除root用户外，其它用户需要在home目录下新建.vimrc


暂定配置，以后要是有需要以vim为主力编辑器，再继续完善！
```shell
  1 " 显示行号
  2 :set number
  3 " 语法高亮
  4 :syntax on
  5 " Tab键的宽度
  6 :set tabstop=4
  7 " 自动缩进
  8 :set cindent
  9 :set autoindent
 10 :set smartindent
 11 " 不和vi兼容
 12 :set nocompatible
 13 " 显示标尺
 14 :set ruler
 15 " 显示状态行
 16 :set laststatus=2
 17 " 状态行格式
 18 :set statusline=%F%m%r%h%w\ [FORMAT=%{&ff}]\ [TYPE=%Y]\ [POS=%l,%v][%p%%]\ %{strftime(\"%d/%m/%y\ -\ %H:%M\")}
 19 " 高亮显示匹配的括号
 20 :set showmatch
 21 " 匹配括号高亮的时间(单位是十分之一秒)
 22 :set matchtime=1
 23 " 使backspace键可以正常处理indent, eol, start等
 24 :set backspace=2
 25 " 搜索逐字高亮
 26 :set hlsearch
 27 :set incsearch
 28 " 编码设置
 29 :set enc=utf-8
```
