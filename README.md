
# 万象系列方案: 适用 IOS 端元书输入法

---------------------

![](https://zycs-img-3ao.pages.dev/v2/SczpHXc.jpeg)

---

### ⌨️ 配置 t9 九键方案

> 👍 原万象拼音(基础版)已经配置好了, 但是并没有打开注释, 需要打开.



> [!NOTE]
> 配置的时候, 尽量打补丁, 这样更新的时候, 自己定义的参数才不会被覆盖.

- <span style="font-weight:bold;">default.custom.yaml</span>

  ```yaml
  # default.yaml 补丁文件
  patch:
    #  设置候选词个数
    menu:
      page_size: 6
    schema_list:
      - schema: wanxiang_t9  # 九键方案
  ```


- <span style="font-weight:bold;">wanxiang_t9.custom.yaml</span>
	
	```yaml
  patch:
    # 拼写设定
    speller:
      # table_translator翻译器，支持自动上屏。例如 “zmhu”可以自动上屏“怎么回事”
      #  auto_select: true
      #  auto_select_pattern: ^[a-z]+/|^[a-df-zA-DF-Z]\w{3}|^e\w{4}
      # 如果不想让什么标点直接上屏，可以加在 alphabet，或者编辑标点符号为两个及以上的映射，alphabet就是将字符纳入输入编码的范畴
      alphabet: zyxwvutsrqponmlkjihgfedcbaZYXWVUTSRQPONMLKJIHGFEDCBA9876543210`/\
      initials: zyxwvutsrqponmlkjihgfedcbaZYXWVUTSRQPONMLKJIHGFEDCBA9876543210
      delimiter: " '"        # 系统配置，第一位<空格>是拼音之间的分隔符；第二位<'>表示可以手动输入单引号来分割拼音。
      visual_delimiter: " "  # super_preedit.lua配置：是否让分隔符号跟着一起转换，例如nǐ'hǎo 在实际使用中表现出视觉拥挤，我们可以让delimiter平时是'转换为拼音的时候使用空格nǐ hǎo，更符合实际。
      tone_isolate: true     # super_preedit.lua配置：是否将数字声调从转换后拼音中隔离出来（true=隔离， false 直接参与转换）例如：nǐ3
      algebra:
        - xform/^(.*);.*$/$1/
        - xlit/āáǎàōóǒòēéěèīíǐìūúǔùǖǘǚǜüńňǹḿm̀/aaaaooooeeeeiiiiuuuuvvvvvnnnmmm/
        - derive/^ng$/eng/
        - xform/^n$/en/
        - xform/^m$/me/
        - derive/^(.*)$/\U$1/
        - derive/^([nl])ve$/$1ue/
        - derive/^([NL])VE$/$1UE/
        - derive/^([jqxy])u/$1v/
        - derive/^([JQXY])U/$1V/
        - xlit/ABCDEFGHIJKLMNOPQRSTUVWXYZ/22233344455566677778889999/
        # ### 九宫格映射 ✍️ 这是原来没有的
        - derive/[abc]/2/
        - derive/[def]/3/
        - derive/[ghi]/4/
        - derive/[jkl]/5/
        - derive/[mno]/6/
        - derive/[pqrs]/7/
        - derive/[tuv]/8/
        - derive/[wxyz]/9/
	```

这样就可以在基本不修改原来文件的基础上完成配置.

---

### 🤔 Some

---

- 📦 [语法模型下载](https://github.com/amzxyz/RIME-LMDG/releases/download/LTS/wanxiang-lts-zh-hans.gram)

- ⌨️ [万象拼音](https://github.com/amzxyz/rime_wanxiang)

- 🧭 [RIME 定制手册(英文)](https://deepwiki.com/sbxlm/librime/5.1-configuration-customization)

- 🧭 [RIME 官方文档](https://github.com/rime/home/wiki/RimeWithSchemata)
