
Viết code Python theo chuẩn
===================

#### Contents
- [Intro](#intro)
- [Setup linters on the popular editors](#setup-linters-on-the-popular-editors)
  - [Visual Studio Code](#visual-studio-code)
  - [Atom](#atom)
  - [Sublime Text 3](#sublime-text-3)
  - [Vim/Neovim](#vimneovim)


## Intro

Trong môi trường phát triển phần mềm hiện nay, việc tuân thủ quy ước chung về coding là rất quan trọng, giúp chương trình trở nên trong sáng, mạch lạc, ít lỗi và dễ chỉnh sửa về sau. Khi làm việc nhóm càng bắt cuộc phải tuân thủ quy ước coding, vì source code chính là nơi các nhà phát triển giao tiếp với nhau.

 Coding convention, hay coding standards, bao gồm 3 vấn đề: 

- *định dạng code* (code formatting): liên quan đến hình thức trình bày ví dụ như dùng khoảng trắng, nhảy dòng, các ký hiệu logic và toán học...
- *quy ước đặt tên* (naming convention): liên quan đến cách đặt tên biến, hàm, lớp...
- *best practices*: đây là kết quả đến từ kinh nghiệm của vô số lập trình viên đi trước, đúc rút ra được những cách viết nào có lợi nhất mà chúng ta nên làm theo

Quy ước viết code có những phạm vi áp dụng dưới đây, theo thứ tự ưu tiên tăng dần:

- convention của cá nhân developer
- convention của công ty, tổ chức
- convention của team
- convention của dự án

Nghĩa là, nếu dự án (và khách hàng trong dự án) không đưa ra yêu cầu riêng về convention, chúng ta sẽ làm theo chuẩn của team mình. Nếu team mình chưa có convention, thì áp dụng theo chuẩn của công ty. Nếu công ty cũng chưa có thì tự áp dụng convention của chính mình hoặc lấy theo 1 chuẩn có sẵn trên mạng (vd [Google Python style guide](https://google.github.io/styleguide/pyguide.html)).

Công ty và team chúng ta lựa chọn chuẩn [PEP 8](https://www.python.org/dev/peps/pep-0008/) cho Python.  

PEP8 có cả 1 danh sách dài các quy tắc, nhưng đây là những điều quan trọng nhất nên thuộc lòng:

- **Shebang**: luôn bắt đầu file với `#!/usr/bin/env python3`
- **File encoding**: UTF-8
- **Indentation**: 4 spaces
- **Maximum line length**: 79
- **Comments**: bắt đầu với `#`, từng hàng một
- **Single quote**: luôn quote bằng nháy đơn khi có thể
-  **Naming conventions**: `CamelCase` for Class name, `UPPERCASE` for constants, otherwise, `lowercase` and `under_score`

Không cần phải nhớ hết các rules, vì đã có nhiều tool hỗ trợ làm việc đó một cách tự động. Chúng được gọi là "linter". Việc tự động tìm lỗi convention trong code gọi là "linting".

Các linters thường hoạt động như CLI tool, hoặc tích hợp vào trong các editors để tự động dò và báo lỗi ngay trong quá trình viết code.

Có ít nhất 3 linters dò lỗi theo chuẩn PEP8 là [pycodestyle]([https://pypi.org/project/pycodestyle/](https://pypi.org/project/pycodestyle/)), [pyflakes]([https://pypi.org/project/pyflakes/](https://pypi.org/project/pyflakes/)) và [flake8](https://pypi.org/project/flake8/). Chúng ta chọn `flake8` vì tool này kết hợp được ưu điểm của cả 2 tools kia.


## Setup linters cho các editor thông dụng

Trước hết, bạn cần cài đặt `flake8`. Trên Ubuntu/Debian, có thể dùng `apt` hoặc `pip3`:

```bash
sudo apt install flake8

# or using pip
sudo pip3 install flake8
```

Sau đó, với mỗi editor, chúng ta làm theo các bước khác nhau để cài đặt và cấu hình.

####  Visual Studio Code

Nhấn tổ hợp `Ctrl` + `Shift` + `X` (hoặc mở  File --> Preferences --> Extensions), hoặc nhấn vào Extensions tab. Gõ từ khóa "python" vào ô tìm kiếm như hình dưới để cài extension Python nếu chưa có.

![enter image description here](https://i.imgur.com/1KBcYiG.png)

Mở Command Paletter bằng tổ hợp phím `Ctrl` + `Shift` + `P` (hoặc View --> Command Palette), nhập vào `Python: Enable Linting`, rồi chọn `On` để kích hoạt linting.

Cũng trên Command Palette, nhập vào `Python: Select Linter`, rồi chọn `flake8` từ danh sách xổ xuống:

![enter image description here](https://i.imgur.com/5qCocsc.png)


Nếu chưa có extension `flake8`, VSCode sẽ gợi ý cài đặt, chỉ việc nhấn "Install" là xong.

![](https://i.imgur.com/mA7Vrfl.png)

Cuối cùng, restart lại VSCode để xem linter đã hoạt động như trong hình bên dưới hay chưa:

![](https://i.imgur.com/i7aO0e0.png)

Nếu muốn tùy biến cách hiển thị, bạn có thể tham khảo thêm các hướng dẫn sau:

- [Linting Python in Visual Studio Code](https://code.visualstudio.com/docs/python/linting)
- [Configure flake8](https://code.visualstudio.com/docs/python/settings-reference#_flake8)


####  Atom

Với Atom, chúng ta cần cài đặt các plugins sau:

- [linter](https://github.com/steelbrain/linter)
- [linter-ui-default](https://github.com/steelbrain/linter-ui-default)
- [intentions](https://github.com/steelbrain/intentions)
- [busy-signal](https://github.com/steelbrain/busy-signal)
- [linter-flake8](https://github.com/AtomLinter/linter-flake8)

Sử dụng lệnh `apm` để cài nhanh:

```bash
apm install linter linter-ui-default intentions busy-signal linter-flake8
```

Sau khi hoàn tất, vào Packages Settings để cấu hình.

*Recommended settings*

- **linter**:
   - Link Preview Tabs: ON
   - Link on Open: ON
   - Link on Change: ON
 - **linter-ui-default**:
   - Always Take Minimum Space: ON
   - Hide Panel When Empty: ON
   - Show Decorations: ON
   - Show Status Bar: ON
   - Show Tooltip: ON
   - Statusbar Represents: Entire Project

![enter image description here](https://i.imgur.com/irUfWlW.png)

####  Sublime Text 3

Với Sublime Text, nếu đã có sẵn [Package Control](https://packagecontrol.io), bạn chỉ cần cài thêm 2 packages  sau:

- [SublimeLinter](https://github.com/SublimeLinter/SublimeLinter)
- [SublimeLinter-flake8](https://github.com/SublimeLinter/SublimeLinter-flake8)

Sau đó tiến hành thiết lập cấu hình.

*Recommended settings*

```json
{
        "default_line_ending": "unix",
        "draw_white_space": "all",
        "ensure_newline_at_eof_on_save": true,
        "show_encoding": true,
        "show_line_endings": true,
        "tab_size": 4,
        "translate_tabs_to_spaces": true,
        "trim_trailing_white_space_on_save": true,
        "word_wrap": "false"
}
```

![enter image description here](https://i.imgur.com/ZWyY75g.png)



#### Vim/Neovim

Với Vim hoặc Neovim sẽ cần cài đặt 3 plugins sau:

- [ALE](https://github.com/w0rp/ale)
- [lightline](https://github.com/itchyny/lightline.vim)
- [lightline-ale](https://github.com/maximbaz/lightline-ale)

Sau đó, chèn thêm đoạn mã dưới đây vào file cấu hình `.vimrc` của Vim hoặc `init.vim` của Neovim:

```vim

let g:lightline = {
      \ 'colorscheme': 'Dracula',
      \ 'active': {
      \   'left': [
      \               ...
      \           ],
      \   'right': [
      \               [ 'linting', 'fileencoding', 'filetype'],
      \   ],
      \ },
      \   'linting': 'LinterStatus',
      \ },
      \ }

function! LinterStatus() abort
    let l:counts = ale#statusline#Count(bufnr(''))

    let l:all_errors = l:counts.error + l:counts.style_error
    let l:all_non_errors = l:counts.total - l:all_errors

    return l:counts.total == 0 ? 'OK' : printf(
    \   '%dW %dE',
    \   all_non_errors,
    \   all_errors
    \)
endfunction

let g:ale_sign_column_always = 1

let g:ale_linters = {
\   'python': ['flake8'],
\}

```

Kết quả thu được sẽ giống như hình:

![](https://i.imgur.com/lTUAKyF.png)


## Conclusion

Linter là trợ lý tin cậy của bạn trong công việc viết code. Sau khi cài đặt và cấu hình linter hoàn tất, việc viết code tuân thủ theo quy ước sẽ trở nên đơn giản hơn nhiều. Các lỗi convention sẽ được editor báo hiệu ngay để bạn kịp thời sửa lại. Đây là điều kiện cơ bản để code chuẩn, code đẹp và code hiệu quả hơn.

___________________
