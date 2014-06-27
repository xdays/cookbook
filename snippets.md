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

#Python技巧
##循环序列元素和索引
    #将序列转换成迭代器
    for index, item in emumerate(sequence):
        if item > 23:
            sequence[index] = transform(item)

##展开嵌套的序列
    def list_or_tuple(x):
        return isinstance(x, (list, tuple))
    def flatten(sequence, to_expand=list_or_tuple):
        for item in sequence:
            if to_expand(item):
                for subitem in flatten(item, to_expand):
                    yield subitem
            else:
                yield item

##二位阵列变换
    arr = [[1,2,3],[4,5,6],[7,8,9]]
    print map(list, zip(\*arr))

##将列表交替作为字典的键值
    def dictFromList(keyAndValue):
        return dict(zip(keyAndValue[::2], keyAndValue[1::2]))

或者更通用的实现：

    def pairwise(iterable):
        itnext = iter(iterable).next
        while True:
            yield itnext(), itnext()
    def dictFromSequence(seq):
        return dict(pairwise(seq))

##反转字典
    def invert_dict(d):
        return dict([ (v, k) for k,v in d.iteritems()])

#排序和搜索
##根据内嵌数字排序
    import re
    def embeded_numbers(s):
        pieces = re_digits.split(s)
        pieces[1::2] = map(int, pieces[1::2])
        return pieces
    def sort_strings_with_embeded_numbers(alist):
        return sorted(alist, key=embeded_numbers)

##增加元素时保持序列顺序
    import heapq
    heapq.heapify(the_list)
    heapq.heappop(the_list)
    heapq.heappush(the_list)

##在已排序的列表中寻找元素
    import bisect
    x_insert_point = bisect.bisect_right(L, x)
    x_is_present = L[x_insert_point-1:x_insert_point] == [x]

##三行实现排序
    #注意这只是演示列表推导式的强大，实际代码应该用sort方法
    def qsort(L):
        if len(L) <= 1: return L
    return qsort([lt for lt in L[1:] if lt < L[0]) + L[0:1] + [ge for ge in L[1:] if ge >= L[0]])

##添加列表不存在的元素
    def addUniqe(baseList, otherList):
        auxDict = dict.fromkeys(baseList)
        for item in otherList:
            if item not in auxDict:
                baseList.append(item)
                auxDict[item] = None

#持久化和数据库
##序列化时压缩
    def cPickle, gzip
    def save(filename, *objects):
        fil = gzip.open(filename, 'wb')
        for obj in objects: cPickle.dump(obj, fil, proto=2)
        fil.close()
    def load(filename):
        fil = gzip.open(filename, 'rb')
        while True:
            try: yield cPickle.load(fil)
            except: EOFError: break
        fil.close()

#系统管理
##统计来访IP
    def caculateApache(logfile_pathname):
        ipHitListing = {}
        contents = open(logfile_pathname, 'r')
        for line in contents:
            ip = line.split(' ', 1)[0]
            if 6 < len(ip) <= 15:
                # 这行可以省去if...else...的逻辑
                ipHitListing[ip] = ipHitListing.get(ip, 0) + 1
        return ipHitListing

#网络编程
##通过socket传输数据
    #server.py
    import socket
    port = 8001
    s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
    s.bind('', port)
    print 'Waiting on port: %s' % port
    while True:
        data, addr = s.recvfrom(1024)
        print 'Received: %s from %s' % (data, addr)

    #client.py
    import socket
    port = 8081
    host = 'localhost'
    s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
    s.sendto("Holy Guido! It's woring.", (host, port))

##判断FTP是否可用
    import socket, ftplib
    def isFTPSiteUp(site):
        try:
            ftplib.FTP(site).quit()
        except socket.error:
            return False
        else:
            return True
