#文本
##每次处理一个字符
    thelist = list(thestring)
    for c in thestring:
        do_some_thing_with(c)
    results = [ do_some_thing_with(c) for c in the string ]
    results = map(do_some_thing_with, thestring)

##字符和字符值转换
    print ord('a')
    print chr('97')

##测试对象是否为类字符串
    def isAString(anobj):
        return isinstance(anobj, basestring)

##合并字符串
    largestring = ''.join(pieces)
    largestring = ='some %s' % thestring

##将字符串逐字符或者词反转
    revchars = asstring[::-1]
    revword = ' '.join(asstring.spilit(' ')[::-1])
    revword = ' '.join(re.split(r'(\s+)', asstring)[::-1])

##检查字符串中是否包含某字符集合的字符
    def containAny(seq, aset)
        for c in seq:
            if c in aset: return True
        return False

##简化字符串的translate方法是用
    import string
    def translator(frm='', to='', delete='', keep=None)
        if len(to) == 1:
            to = to * len(frm)
        trans = string.maketrans(frm, to)
        if keep is not None:
            allchars = string.maketrans('', '')
            # 要删除的字符->要保留的字符->要删除的字符, 主要是处理keep和delete的逻辑
            delete = allchars.translate(allchars, keep.translate(allchars, delete))
        def translate(s):
            return s.translate(trans, delete)
        return tranlate

##过滤字符串中不属于指定集合的字符
    import string
    # 无需翻译
    allchars = string.maketrans('', '')
    def makefilter(keep):
        #取反
        delchars = allchars.translate(allchars, keep)
        def thefilter(s):
            #再取反
            return s.translate(allchars, delchars)
        return thefilter

##检查对象是文本还是二进制
    from __futurn__ import division
    import string
    text = ''.join(map(chr, range(32,127))) + '\n\r\t\b'
    _null_trans = string.maketrans('', '')
    def is_text(s, text=text, threshold=0.30):
        if '\0' in s:
            return False
        if not s:
            return False
        t = s.translate(_null_trans, text)
        return len(t)/len(s) <= threshold

##一次完成多次替换
    import re
    def make_xlat(*args, **kwds)
        adict = dict(*args, **kwds)
        rx = re.compile('|'.join(map(re.escape, adict)))
        def one_xlat(match):
            return adict[match.group(0)]
        def xlat(text):
            return rx.sub(one_xlat, text)
        return xlat

##检查字符串中的结束标记
    import itertools
    def anyTrue(predicate, sequence):
        return True in itertools.imap(predicate, sequence)
    def endsWith(s, *endings):
        return anyTrue(s.endswith, endings)

