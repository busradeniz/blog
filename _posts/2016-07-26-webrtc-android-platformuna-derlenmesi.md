---
id: 79
title: WebRTC Android Platformuna Derlenmesi
date: 2016-07-26T12:30:02+01:00
author: Busra Deniz
layout: post
guid: http://busradeniz.com/?p=79
permalink: /webrtc-android-platformuna-derlenmesi/
asalah_show_meta:
  - "0"
asalah_show_share:
  - "0"
asalah_show_title:
  - "0"
show_author_box:
  - "0"
asalah_custom_description:
  - ""
asalah_sidebar_position:
  - "0"
socialcount_TOTAL:
  - "0"
socialcount_facebook:
  - "0"
socialcount_linkedin:
  - "0"
socialcount_reddit:
  - "0"
socialcount_stumbleupon:
  - "0"
social_aggregate_score:
  - "0"
social_aggregate_score_detail:
  - 'a:4:{s:5:"total";d:0;s:13:"social_points";i:0;s:11:"view_points";d:0;s:14:"comment_points";i:0;}'
social_aggregate_score_decayed:
  - ""
social_aggregate_score_decayed_last_updated:
  - "1528578489"
socialcount_LAST_UPDATED:
  - "1528578489"
image: /wp-content/uploads/2017/07/webrtc_android_build_title-825x510.png
categories:
  - iOS
  - WebRTC
tags:
  - webrtc android compile
  - webrtc android derleme
  - webrtc compile for android
  - webrtc mobile
  - webrtc nasıl derlenir
  - webrtc native android
  - webrtc türkçe
  - webrtc türkçe kaynak
---
<p class="graf graf--p">
  <img class="aligncenter size-full wp-image-80" src="http://busradeniz.com/wp-content/uploads/2017/07/webrtc_android_build_title.png" alt="" width="960" height="640" srcset="https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_android_build_title.png 960w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_android_build_title-300x200.png 300w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_android_build_title-768x512.png 768w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_android_build_title-600x400.png 600w" sizes="(max-width: 960px) 100vw, 960px" />WebRTC kütüphanesini <a class="markup--anchor markup--p-anchor" href="http://busradeniz.com/2016/07/23/webrtc-ios-platformuna-derlenmesi/" target="_blank" rel="noopener" data-href="https://medium.com/@busradeniz/webrtc-ios-platformuna-derlenmesi-70a4d039bbcb#.vm3ermduy">iOS platformuna derledikten</a> sonra aynı işlemleri Android için de yapmamız gerekiyor. iOS ile benzer adımlarla Android için de derleme işlemini yapıyoruz ama tabiki ortam gerekliliklerinde bazı farklılıklar var.
</p>

### Ortam Gereklilikleri {.graf.graf--h3}

<p class="graf graf--p">
  WebRTC Android derlemesi için Linux bir makineye ihtiyaç duyacaksınız. Ben ilk olarak AWS’de bir Ubuntu makine ayağa kaldırıp o makine üzerinde derlemeye çalıştım fakat makinenin özellikleri derleme işlemi için yeterli olmadı. Bunun üzerine kendi makineme Vagrant kurarak ilerledim. Daha önce Vagrant kullanmama rağmen <a class="markup--anchor markup--p-anchor" href="http://sourabhbajaj.com/mac-setup/Vagrant/README.html" target="_blank" rel="noopener" data-href="http://sourabhbajaj.com/mac-setup/Vagrant/README.html">buradaki blog yazısı</a> ile çok basit ve sıkıntısız adımlarla ilerleyebildim. Sadece <strong class="markup--strong markup--p-strong"><em class="markup--em markup--p-em">vagrant up</em></strong> komutunu çalıştırmadan önce <strong class="markup--strong markup--p-strong"><em class="markup--em markup--p-em">Vagrantfile</em></strong> dosyasında aşağıdaki gibi değişiklik yaptım.
</p>

<pre name="7cdd" class="graf graf--pre">config.vm.provider "virtualbox" do |vb|
     vb.memory = 4096
end</pre>

<p class="graf graf--p">
  Makinenin Ubuntu versiyonu :
</p>

<pre name="8e6e" class="graf graf--pre">$ lsb_release -a
Distributor ID:	Ubuntu
Description:	Ubuntu 12.04 LTS
Release:	12.04
Codename:	precise</pre>

<p class="graf graf--p">
  Ve tabiki hemen sonrasında makineye Git kurmamız gerekiyor :
</p>

<pre name="39e5" class="graf graf--pre">$ apt-get install git</pre>

<pre name="0c3b" class="graf graf--pre">// Git kurulumundan sonra 
$ git --version
git version 1.7.9.5</pre>

<p class="graf graf--p">
  Böylelikle geliştirme ortamımız derleme için hazır hale geldi.
</p>

### WebRTC kodunu alma {.graf.graf--h3}

<p class="graf graf--p">
  Burdan sonraki adımlar iOS derleme işlemleriyle çok benzer şekilde ilerliyor. Yine öncesinde <strong class="markup--strong markup--p-strong"><em class="markup--em markup--p-em">depot_tools</em></strong> script paketini indiriyoruz.
</p>

<pre name="1360" class="graf graf--pre">$ git clone <a class="markup--anchor markup--pre-anchor" href="https://chromium.googlesource.com/chromium/tools/depot_tools.git" target="_blank" rel="noopener" data-href="https://chromium.googlesource.com/chromium/tools/depot_tools.git">https://chromium.googlesource.com/chromium/tools/depot_tools.git</a></pre>

<p class="graf graf--p">
  Ardından PATH değişkenimizi tanımlıyoruz :
</p>

<pre name="7897" class="graf graf--pre">$ export PATH=`pwd`/depot_tools:"$PATH"</pre>

<p class="graf graf--p">
  PATH değişkenimi yazdırdığımda şu şekilde bir sonuç elde ediyorum.
</p>

<p class="graf graf--p">
  <em class="markup--em markup--p-em">/home/vagrant/webrtc/depot_tools:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/opt/vagrant_ruby/bin</em>
</p>

<p class="graf graf--p">
  Target işletim sistemini Android olarak belirtip, sonrasında fetch ve sync komutlarını sırayla çalıştırıyoruz
</p>

<pre name="83a8" class="graf graf--pre">$ export GYP_DEFINES="OS=android"

</pre>

<pre name="237d" class="graf graf--pre">$ fetch --nohooks webrtc_android
$ gclient sync</pre>

<p class="graf graf--p">
  <strong class="markup--strong markup--p-strong"><em class="markup--em markup--p-em">gclient sync</em></strong> komutunun işlemleri yaklaşık 6 saat sonra tamamlandı ve yaklaşık 22 GB’lık kod indirildi. Ardından adb vethird_party/android_tools altındaki android toollarını PATH’e eklemek için aşağıdaki komutu çalıştırıyoruz.
</p>

<pre name="ea23" class="graf graf--pre">$ . build/android/envsetup.sh</pre>

### Kodun Derlenmesi {.graf.graf--h3}

<p class="graf graf--p">
  Kodu lokalinize aldıktan sonra yine GYP değişkenlerini tanımlamanız ve ardından da <strong class="markup--strong markup--p-strong"><em class="markup--em markup--p-em">gclient runhooks</em></strong> komutunu çalıştırmamız gerekiyor. <strong class="markup--strong markup--p-strong"><em class="markup--em markup--p-em">gclient runhooks</em></strong> komutundan sonra <strong class="markup--strong markup--p-strong"><em class="markup--em markup--p-em">src</em></strong> klasörü içerisinde tanımladığınız <strong class="markup--strong markup--p-strong"><em class="markup--em markup--p-em">output_dir</em></strong> klasörü oluşacaktır.
</p>

<pre name="d21e" class="graf graf--pre">//GYP değişkenlerinin tanımlanması
$ export GYP_DEFINES="OS=android $GYP_DEFINES"</pre>

<pre name="7cd5" class="graf graf--pre">$ export GYP_GENERATOR_FLAGS="$GYP_GENERATOR_FLAGS output_dir=out_android"

</pre>

<pre name="39f6" class="graf graf--pre">// .ninja dosyalarının yaratılması için runhooks komutunu çalıştırıyoruz.
$ gclient runhooks</pre>

<p class="graf graf--p">
  Ortam değişkenlerimizin tanımlanmasından sonra kodu build etme aşamasına geliyoruz. <strong class="markup--strong markup--p-strong"><em class="markup--em markup--p-em">src</em></strong> klasörünün içinde olduğumuzdan emin olduktan sonra build komutunu koşabiliriz. Burdaki <strong class="markup--strong markup--p-strong"><em class="markup--em markup--p-em">GYP_GENERATOR_FLAGS</em></strong> değişkeninde <strong class="markup--strong markup--p-strong"><em class="markup--em markup--p-em">output_dir</em></strong> olarak tanımladığınız değerden ve istediğiniz build modunun (Debug-Release) doğruluğundan emin olmanız gerekiyor.
</p>

<pre name="2ba6" class="graf graf--pre">// AppRTCDemo debug modunda build etme 
ninja -C out_android/Debug AppRTCDemo</pre>

<pre name="3c54" class="graf graf--pre">//Build edilen AppRTCDemo çalıştırma
adb install -r out_android/Debug/apks/AppRTCDemo.apk</pre>

<p class="graf graf--p">
  Ve böylelikle elinizde Android için derlemiş olduğunuz webrtc kütüphanesi ve örnek uygulama AppRTCDemo var.
</p>