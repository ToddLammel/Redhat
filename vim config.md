除root用户外，其它用户需要在home目录下新建.vimrc


暂定配置，以后要是有需要以vim为主力编辑器，再继续完善！
```shell
" 显示行号
:set number
" 语法高亮
:syntax on
" Tab键的宽度
:set tabstop=4
" 自动缩进
:set cindent
:set autoindent
:set smartindent
" 不和vi兼容
:set nocompatible
" 显示标尺
:set ruler
" 显示状态行
:set laststatus=2
" 状态行格式
:set statusline=%F%m%r%h%w\ [FORMAT=%{&ff}]\ [TYPE=%Y]\ [POS=%l,%v][%p%%]\ %{strftime(\"%d/%m/%y\ -\ %H:%M\")}
" 高亮显示匹配的括号
:set showmatch
" 匹配括号高亮的时间(单位是十分之一秒)
:set matchtime=1
" 使backspace键可以正常处理indent, eol, start等
:set backspace=2
" 搜索逐字高亮
:set hlsearch
:set incsearch
" 编码设置
:set enc=utf-8
```
