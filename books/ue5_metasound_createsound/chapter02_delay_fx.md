---
title: "DelayでFX（エフェクト）をかける"
---

## DelayでFX（エフェクト）をかける

使用するノードは[Delay] [Stereo Delay]ノードです。

![](/images/books/ue5_metasound_createsound/chapter02_delay_fx/2022-02-19-19-14-20.png)
*[Delay] [Stereo Delay]*

前回作成した MetaSoundを複製して、[MS_Procedual05]を作成します。

![](/images/books/ue5_metasound_createsound/chapter02_delay_fx/2022-09-29-07-08-22.png)

最終出力に使用している[AudioのMultiply]からドラッグ&ドロップして[Delay]を追加します。

![](/images/books/ue5_metasound_createsound/chapter02_delay_fx/2022-09-29-07-10-42.png)
*最終出力に使用している[AudioのMultiply]からドラッグ＆ドロップ > Delay*

[Delay]ノードのパラメーターをInput化します。
パラメーターからドラッグ&ドロップして、[Promote To Graph Input]を選択します。

![](/images/books/ue5_metasound_createsound/chapter02_delay_fx/2022-09-29-07-13-14.png)
*パラメーターからドラッグ＆ドロップ > [Promote To Graph Input]を選択*

Input Nameを[Mono （パラメーター）]になるように変更します。

![](/images/books/ue5_metasound_createsound/chapter02_delay_fx/2022-09-29-07-15-00.png)
*Input Name：Mono (パラメーター名)*

最終出力に使用している[AudioのMultiply]からドラッグ&ドロップして[Stereo Delay]を追加します。

![](/images/books/ue5_metasound_createsound/chapter02_delay_fx/2022-09-29-07-16-36.png)
*最終出力に使用している[AudioのMultiply]からドラッグ＆ドロップ > [Stereo Delay]を追加*

[Stereo Delay]はStereo出力なので、[MetaSound]をクリックして、OutputFormatを[Stereo]に変更してMono出力からStereo出力に変更します。

![](/images/books/ue5_metasound_createsound/chapter02_delay_fx/2022-09-29-07-19-02.png)
*MetaSound > OutputFormatを[Stereo]に変更*

再生してからパラメーターを調整できるようにパラメーターをインプット化します。Input Nameは[Stereo （インプット名）]に設定します。

![](/images/books/ue5_metasound_createsound/chapter02_delay_fx/2022-09-29-07-40-29.png)
*Stereo DelayからAudioを出力するようにする*

Delayノードでは音を遅らせることができます。
Delayノードで音を遅らせてStereo化することで左側の音を遅らせて、右側の音とズレを発生させています。

![](/images/books/ue5_metasound_createsound/chapter02_delay_fx/2022-09-29-07-42-10.png)
*Stereo化させることで右と左の音にズレを発生させる*

Stereo Delayではずらした左と右のズレを調整しています。

![](/images/books/ue5_metasound_createsound/chapter02_delay_fx/2022-09-29-07-43-28.png)
*Stereo Delayではズレている音を調整している*

https://masatsumu-dtm.com/word_57-delay/

https://twitter.com/posita33/status/1469317121004150787
