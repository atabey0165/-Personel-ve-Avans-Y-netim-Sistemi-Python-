
[personel-takip.py](https://github.com/user-attachments/files/22454686/personel-takip.py)
from datetime import datetime
liste=[]

def menü():
  while True:  
    print("\n1-yeni personel ekle")
    print("2-personel listesini göster")
    print("3-avans çikişi")
    print("4-avans geçmişleri")
    print("5-personel silme")
    print("6-çikiş")
    seçim=input("yapmak istediğiniz işlem numarasini seçin: ")
    if seçim=="1":
        yeni_personel_ekle()
    elif seçim=="2":
        personel_listesini_göster()
    elif seçim=="3":
        avans_çikişi()
    elif seçim=="4":
        avans_geçmişi()        
    elif seçim=="5":
        personel_silme()
    
    elif seçim=="6":
        print("çikiş yapiliyor..")
        break
    else:
        print("hatali seçim lütfen 1/7 arasi bir seçim yapin") 

def yeni_personel_ekle():
    isim=input("ad soyad: ")
    maaş=int(input("maaşi: "))
    tel=input("telefon no: ")
    görev=input("çalişma alani: ")
    liste.append({"ad soyad":isim,"maaşi":maaş,"telefon":tel,"çalişma alani":görev,"avanslar":[]})
    print(f"{isim} eklendi,maaşi:{maaş}")

def personel_listesini_göster():
    if not liste:
        print("liste boş listelenemez")
        return
    for no ,s in enumerate(liste,1):
        print(f"{no}. Ad Soyad: {s['ad soyad']}, Maaş: {s['maaşi']} TL, Tel: {s['telefon']}, Alan: {s['çalişma alani']}")

def avans_çikişi():
   if not liste:
      print("liste boş ödeme yapilamaz")
      return
   personel_listesini_göster()
   try:
      seçilen_no=int(input("personel numarasi seçin: "))
      if 1<=seçilen_no<=len(liste):
         seçim=liste[seçilen_no-1]
         tutar=float(input("avans  miktar: "))
         if tutar<=seçim['maaşi']:
            seçim['maaşi']-=tutar
            tarih = datetime.now().strftime("%d.%m.%Y")
            seçim["avanslar"].append({"tutar": tutar, "tarih": tarih})
            print(f"{seçim['ad soyad']} için {tutar} tl ödeme yapildi kalan maaşi: {seçim['maaşi']}")
         else:
            print("maaş üzeri ödeme yapilamaz")
      else:
        print("geçersiz personel numarasi")        
   
   except ValueError:
      print("geçerli bir sayi girin")   

def avans_geçmişi():
    if not liste:
       print("liste boş avans geçmişi siralanamaz")
       return
    personel_listesini_göster()
    no=int(input("avans geçmişini görmek istediğiniz personel numarasini girin: "))
    try:  
     if 1<=no<=len(liste):
       seç=liste[no-1]
       if seç['avanslar']:
          print(f"\n{seç['ad soyad']} avans geçmişi")
          for n,i in enumerate(seç['avanslar'],1):
             print(f"{n}-{i['tutar']} tl {i['tarih']}")
       else:
        print("Bu personelin henüz avansı yok.")
     else:
      print("Geçersiz seçim.")      
    except ValueError:
     print("geçerli sayi girin")

def personel_silme():
   if not liste:
       print("liste boş silme yapilamaz")
       return
   personel_listesini_göster()
   try: 
    silinecek_no=int(input("silmek istediğiniz personel numarasini girin: "))
    if 1<=silinecek_no<=len(liste):
       sil=liste.pop(silinecek_no-1)
       print(f"{sil['ad soyad']} listeden silindi")
    else:
       print("geçerli no girin")    
   except ValueError: 
    print("geçerli bir sayi girin")   


menü()


   
  


    

    
            
