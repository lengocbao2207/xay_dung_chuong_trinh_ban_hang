import os
import datetime



print('+--------------------MENU----------------+')
print('| Chon THH de tao hang hoa               |')
print('| Chon XHH de xem hang hoa               |')
print('| Chon TLH de tao loai hang hoa          |')
print('| Chon XLH de xem loai hang hoa          |')
print('| Chon C de tao hoa don                  |')
print('| Chon R de xem thong tin hoa don        |')
print('| Chon T de tinh tong doanh thu          |')
print('| Chon A de tinh tong hang hoa ban ra    |')
print('| Chon E de thoat                        |')
print('+----------------------------------------+')

danhsachhanghoa=[]
danhsachloaihanghoa=[]
danhsachhoadon=[]

def check_id_nguoidung():
    
	with open('day6/danhmuc/loaihanghoa.csv','r') as f:
		line=f.readline()	

		hoi_id=input('Ban da co id chua: Y/N ')
		if hoi_id.upper()=="Y":
			pass
		if hoi_id.upper()=='N':
			print('Moi ban tao tai khoan: ')
			id=input('Moi nhap id nguoi dung: ')
			pass_word=input('Pass: ')

		

	

def load_loaihanghoa_luckhoidong():
    #da xong ham nay
	files=os.listdir("day6/danhmuc")
	if "loaihanghoa.csv" not in files:
		return


	with open('day6/danhmuc/loaihanghoa.csv','r') as f:
		line=f.readline()
		while line:
			str_to_reads=line.split("#")
			#print("str_to_reads:",str_to_reads)
			if len(str_to_reads) >1:
				loaihanghoa={}
				loaihanghoa['id']=str_to_reads[0]
				tenloai=str_to_reads[1]
				if tenloai.endswith('\n'):
					tenloai=tenloai[0:len(tenloai)-1]
				loaihanghoa['ten']=tenloai
				danhsachloaihanghoa.append(loaihanghoa)
			line=f.readline()
		print('danhsachloaihanghoa:',danhsachloaihanghoa)

def load_hanghoa_luckhoidong():
    # da xong ham nay
	files=os.listdir("day6/danhmuc")
	if "hanghoa.csv" not in files:
		return

	print('      BANG MA VA GIA BAN HANG HOA ')
	print('+----------+----------+---------------+')
	print('|   ID     |    ten   |  gia ban      |')
	print('+----------+----------+---------------+')
	with open('day6/danhmuc/hanghoa.csv','r') as f:
		line=f.readline()
		
		while line:
			str_to_reads=line.split('#')
			#print('str_to_reads',str_to_reads)
			if len(str_to_reads) >1:
				hanghoa={}
				hanghoa['id']=str_to_reads[0]
				hanghoa['ten']=str_to_reads[1]
				hanghoa['giaban']=str_to_reads[2]
				hanghoa['loaihanghoa_id']=str_to_reads[3]

				if hanghoa['loaihanghoa_id'].endswith('\n'):
					hanghoa['loaihanghoa_id']=hanghoa['loaihanghoa_id'][0:len(hanghoa['loaihanghoa_id'])-1]
				danhsachhanghoa.append(hanghoa)
			line=f.readline()
			for i in range(len(hanghoa['id']),10):
				hanghoa['id']=hanghoa['id']+' '
			for i in range(len(hanghoa['ten']),10):
				hanghoa['ten']=hanghoa['ten']+' '
			for i in range(len(hanghoa['giaban']),15):
				hanghoa['giaban']=hanghoa['giaban']+' '
		
			print('|'+hanghoa['id']+'|'+hanghoa['ten']+'|'+hanghoa['giaban']+'|')
			print('+----------+----------+---------------+')
		#print('danhsachhanghoa:',danhsachhanghoa)
load_hanghoa_luckhoidong()

def tao_loaihanghoa():
	#da xong ham nay
	data={}
	id=input('xin moi nhap id loai hang hoa:')
	tim_id_daco=xem_loaihanghoa(id)
	if tim_id_daco is None:
		print('Da ton tai Ma loai hang hoa nay. Xin moi ban thuc hien chuc nang khac')
		return
	else:
		data['id']=id
		data['ten']=input('xin moi nhap ten loai hang hoa:')
		danhsachloaihanghoa.append(data)
		str_to_save=data['id']+'#'+data['ten']+'\n'
		with open('day6/danhmuc/loaihanghoa.csv','a')as f:
			data=f.write(str_to_save)


def xem_loaihanghoa(id=None):
    #da xong ham nay
	if id is None:
		id=input('Xin moi nhap ID loai hang hoa:')
	for loai in danhsachloaihanghoa:
		if loai['id']==id:
			print('loai hang hoa:',loai)
			return loai
		else:
			print('ID hang hoa khong ton tai !')
			#print(danhsachloaihanghoa)

def sua_loaihanghoa(id,data):
	pass
def xoa_loaihanghoa(id):
	pass
def danhsach_loaihanghoa():
	return danhsachloaihanghoa

def tao_hanghoa():
    #ham nay chua on lam
	data={}
	id=input('Xin moi nhap ID hang hoa')
	tim_id_daco=xem_hanghoa(id)
	if tim_id_daco is not None:
		print('Da ton tai Ma loai hang hoa nay. Xin moi ban thuc hien chuc nang khac')
		return
	else:
		data['id']=id
		data['ten']=input('Xin moi nhap ten hang hoa:')
		data['giaban']=input('Xin moi nhap gia ban:')
		loaihanghoa_id=input('Xin moi nhap Ma loai hang hoa:')

	co_hienthidanhsachloai=False
	tim_idloai_daco=xem_loaihanghoa(loaihanghoa_id)

	#while tim_idloai_daco is None:
		#print('Danh sach loai hang hoa:')
		#for loaihanghoa in danhsachloaihanghoa:
		#	print(loaihanghoa['id'])
		#loaihanghoa_id=input('Xin moi nhap ma loai hang hoa:')
		#=xem_loaihanghoa(loaihanghoa_id)



	data['loaihanghoa_id']=loaihanghoa_id
	danhsachhanghoa.append(data)
	str_to_save=data['id']+'#'+data['ten']+'#'+data['giaban']+'#'+data['loaihanghoa_id']+'\n'
	with open('day6/danhmuc/hanghoa.csv','a')as f:
		data=f.write(str_to_save)

	
def xem_hanghoa(id=None):
    #ham nay chua duoc on cho lam 
	if id is None:
		id=input('Xin moi nhap id hang hoa:')
	for hanghoa in danhsachhanghoa:
		if hanghoa['id']==id:
			print(hanghoa)
			return hanghoa
		else:
			print('ID hang hoa khong ton tai ! Moi nhap lai !')


hanghoaban={}

load_loaihanghoa_luckhoidong()

def in_hoa_don():
	print('					HOA DON MUA HANG			')
	print('So hoa don: ',hoadon['sohoadon'])
	print('Ngay mua hang: ',hoadon['ngayhoadon'])
	print('Ten khach hang: ',hoadon['nguoimua'])
	print('_______________________THONG TIN HOA DON______________')
	print('+----------+------------------+----------+---------------+---------------+')
	print('|   STT    |   ten hang hoa   | so luong |   don gia     |   thanh tien  |')
	print('+----------+------------------+----------+---------------+---------------+')

	for hanghoa in hoadon['danhsachhanghoa']:
		#print('in dong hang hoa o day')
		stt=stt+1
		for i in range(len(stt),10):
			stt=stt+' '
		for i in range(len(ten),18):
			ten=ten+' '
		for i in range(len(soluong),10):
			soluong=soluong+' '
		for i in range(len(dongia),15):
			dongia=dongia+' '
		for i in range(len(thanhtien),15):
			thanhtien=thanhtien+' '

		print('|'+stt+'|'+ten+'|'+soluong+'|'+dongia+'|'+thanhtien+'|')
		print('+----------+------------------+----------+---------------+---------------+')
					
	for i in range(len(tongtien),15):
		tongtien=' '+tongtien
	print(' 										|   tong tien   |'+tongtien+'|')
	print(' 										+---------------+---------------+')


while True:
	x=input('=> Chon chuc nang: ')
	print('Ban da chon chuc nang: ',x)
	if x.upper()=='TLH':
		tao_loaihanghoa()
	if x.upper()=='XLH':
		xem_loaihanghoa()
	if x.upper()=='THH':
		tao_hanghoa()
	if x.upper()=='XHH':
		xem_hanghoa()
	if x.upper()=='C':
		print('Moi ban tao hoa don:')
		hoadon={}
		#hoadon={'sohoadon':input('moi nhap so hoa don: )
				#'ngayhoadon':input('moi nhap ngay hoa don: )
				#'nguoimua':input('moi nhap ten nguoi mua: ')
				#'danhsachhanghoa':[]
				#}
		
		sohoadon=input('moi nhap so hoa don: ')
		hoadon['sohoadon']=sohoadon + ' : ' +datetime.datetime.now()
		hoadon['ngayhoadon']=datetime.datetime.now()
		hoadon['nguoimua']=input('moi nhap ten nguoi mua: ')
		hoadon['tongtientruocthue']=0
		hoadon['thue']=0.1
		hoadon['tongtien']=0
		hoadon['danhsachhanghoa']=[]
		nhaphanghoa=input('=> Ban co muon nhap hang hoa khong (Y/N): ')
		stt=0
		while nhaphanghoa.upper()=='Y':
			hanghoa_new={}
			stt=stt+1
			stt_cp=str(stt)
			hanghoa_new['id']=input('Moi nhap id hang hoa: ')
			#for hanghoa in danhsachhanghoa:
    			#if hanghoa['id']==hanghoa_new['id']:

			#with open('day6/danhmuc/hanghoa.csv','r') as f:
				#line=f.readline()
				#while line:
    				#=line.split('#')
					#print('str_to_reads',str_to_reads)
					#if len(str_to_reads) >1:
					#	hanghoa={}
					#	hanghoa['id']=str_to_reads[0]
					#	hanghoa['ten']=str_to_reads[1]
					#	hanghoa['giaban']=str_to_reads[2]

					#if hanghoa['id']==hanghoa_new['id']:
    				#	hanghoa['ten']=hanghoa_new['ten']
					#	hanghoa['giaban']=hanghoa_new['giaban']

			hanghoa_new['ten']=input('Nhap ten loai hang hoa: ')
			soluong=input('nhap so luong: ')
			hanghoa_new['soluong']=int(soluong)
			dongia=input('nhap don gia: ')
			hanghoa_new['dongia']=int(dongia)
			hanghoa_new['thanhtien']=hanghoa_new['soluong']*hanghoa_new['dongia']
			thanhtien=str(hanghoa_new['thanhtien'])

			if hanghoa_new['ten'] in hanghoaban:
				hanghoaban[hanghoa_new['ten']]['tongso']=hanghoaban[hanghoa_new['ten']]['tongso']+hanghoa_new['soluong']
				hanghoaban[hanghoa_new['ten']]['doanhthu']=hanghoaban[hanghoa_new['ten']]['doanhthu']+hanghoa_new['thanhtien']
			else:
				hanghoaban[hanghoa_new['ten']]={
					'tongso':hanghoa_new['soluong'],
					'doanhthu':hanghoa_new['thanhtien']
				}

			hoadon['danhsachhanghoa'].append(hanghoa_new)

			hoadon['tongtientruocthue']=hoadon['tongtientruocthue']+hanghoa_new['thanhtien']

			nhaphanghoa=input('=> Ban co muon nhap hang hoa khong (Y/N):: ')

		hoadon['tongtien']=hoadon['tongtientruocthue']+hoadon['tongtientruocthue']*hoadon['thue']
		danhsachhoadon.append(hoadon)

		#print('danh sach hoa don: ',danhsachhoadon)
		
		#in_hoa_don()
		print('					HOA DON MUA HANG			')
		print('So hoa don: ',hoadon['sohoadon'])
		print('Ngay mua hang: ',hoadon['ngayhoadon'])
		print('Ten khach hang: ',hoadon['nguoimua'])
		print('_______________________THONG TIN HOA DON______________')
		print('+----------+------------------+----------+---------------+---------------+')
		print('|   STT    |   ten hang hoa   | so luong |   don gia     |   thanh tien  |')
		print('+----------+------------------+----------+---------------+---------------+')

		for hanghoa in hoadon['danhsachhanghoa']:
			#print('in dong hang hoa o day')
			#stt=stt+1
			for i in range(len(stt_cp),10):
				stt_cp=stt_cp+' '
			for i in range(len(hanghoa['ten']),18):
				hanghoa['ten']=hanghoa['ten']+' '
			for i in range(len(soluong),10):
				soluong=soluong+' '
			for i in range(len(dongia),15):
				dongia=dongia+' '
			for i in range(len(thanhtien),15):
				thanhtien=thanhtien+' '

			print('|'+   stt_cp+'|'+hanghoa['ten']+'|'+soluong+'|'+dongia+'|'+thanhtien+'|')
			print('+----------+------------------+----------+---------------+---------------+')
		tongtien=str(hoadon['tongtien'])			
		for i in range(len(tongtien),15):
			tongtien=tongtien+' '
		print(' 					 |   tong tien   |'+tongtien+'|')
		print(' 					 +---------------+---------------+')
	
		print('						cam on quy khach hang')
		#print('Kiem tra: ',danhsachhoadon)

		filename='HD'+ hoadon['sohoadon']+'.json' 


	if x.upper()=='R':
		timthay==False
		while timthay is False:
			sohoadon_canxem=input('Nhap so hoa don can xem: ')
			for hoadon in danhsachhoadon:
				if hoadon['sohoadon']==sohoadon_canxem:
					timthay=True
					#hoa don se in o day
					in_hoa_don()
					break
	if x.upper()=='T':
		tongdoanhthu=0
		for hoadon in danhsachhoadon:
			tongdoanhthu=tongdoanhthu+hoadon['tongtien']
		print('Tong doanh thu la: ',tongdoanhthu)

	if x.upper()=='A':
		tongsohanghoa=0
		doanhsoban=0

		tenhanghoa=input('Nhap ten hang hoa can xem: ')
		for hoadon in danhsaachhoadon:
			for hanghoa in hoadon['danhsachhanghoa']:
				if hanghoa['ten']==tenhanghoa:
					tongsohanghoa=tongsohanghoa+hanghoa['soluong']
					doanhsoban=doanhsoban+hanghoa['thanhtien']
					break
		print('Tong so hang hoa: ',tongsohanghoa)
		print('Doanh so ban: ',doanhsoban)

	if x.upper()=='E':
		print('Tam biet ! Hen gap lai !!!')
		print(' 	(^.^)      ')
		break
