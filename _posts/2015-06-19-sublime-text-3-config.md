---
layout: post
title: Sublime Text 3 配置
---

一个自用的Linux版Sublime Text 3 配置文件<!-- more -->

    {
        "color_scheme": "Packages/User/Solarized (Dark) (SL) (Flake8Lint).tmTheme",
        "ensure_newline_at_eof_on_save": true,
        "font_face": "mono",
        "font_size": 14,
        "highlight_line": true,
        "ignored_packages":
        [
        ],
        "indent_to_bracket": true,
        "line_numbers": true,
        "rulers":
        [
            80,
            95,
            120
        ],
        "spell_check": false,
        "tab_size": 4,
        "theme": "Seti.sublime-theme",
        "translate_tabs_to_spaces": true,
        "trim_trailing_white_space_on_save": true
    }

    [
    { "keys": ["j", "j"], "command": "exit_insert_mode",
        "context":
        [
            { "key": "setting.command_mode", "operand": false },
            { "key": "setting.is_widget", "operand": false }
        ]
    },
    { "keys": ["ctrl+alt+up"], "command": "select_lines", "args": {"forward": false} },
    { "keys": ["ctrl+alt+down"], "command": "select_lines", "args": {"forward": true} },
    ]
