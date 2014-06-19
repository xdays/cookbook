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
    def make_xlat(\*args, **kwds)
        adict = dict(\*args, **kwds)
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

#文件
##处理字符串中的zip文件
    import cStringIO, zipfile
    class zipString(zipfile.ZipFile):
        def __init__(self, datastring):
            ZipFile.__init__(self, cStringIO.StringIO(datastring))

##将文件树归档到一个tar文件
    import tarfile, os
    def make_tar(folder_to_backup, dest_folder, commpression='bz'):
        if commpression:
            dest_ext = '.' + compress
        else:
            dest_ext = ''
        arcname = os.path.basename(folder_to_backup)
        dest_name = '%s.tar%s' % (arcname, dest_ext)
        dest_path = os.path.join(dest_folder, dest_name)
        if commpression:
            dest_cmp = ':' + compression
        else:
            dest_cmp = ''
        out = tarfile.TarFile.open(dest_path, 'w'+dest_cmp)
        out.add(folder_to_backup, arcname)
        out.close()
        return dest_path

##遍历目录树
    import os, fnmatch
    def all_files(root, patterns='*', single_level=False, yield_folders=False):
        patterns = patterns.split(';')
        for path, subdirs, files in os.walk(root):
            if yield_folders:
                files.extend(subdirs)
            files.sort()
            for name in files:
                for pattern in patterns:
                    if fnmatch.fnmatch(name, pattern):
                        yield os.path.join(path, name)
                        break
            if sinle_level:
                break

#日期和事件
##计算昨天和明天的日期
    import datetime
    today = datetime.date.today()
    yesterday = today - datetime.timedelta(days=1)
    tomorrow = today + datetime.timedelta(days=1)
    print yesterday, today, tomorrow

##定时执行命令
    import time, os, sys, sched
    schedule = sched.scheduler(time.time, time.sleep)
    def perform_command(cmd, inc):
        schedule.ender(inc, 0, perform_command, (cmd, inc))
        os.system(cmd)
    def main(cmd, inc=60):
        schedule.enter(0, 0, perform_command, (cmd, inc))
        schedule.run()
    if __name__ == '__main__':
        numargs = len(sys.argv) -1
        if numargs < 1 or numargs > 2:
            print 'usage: ' +  sys.argv[0] + ' command [seconds_delay]'
            sys.exit(1)
        cmd = sys.argv[1]
        if numbargs < 3:
            main(cmd)
        else:
            inc = int(sys.argv[2])
            main(cmd, inc)
