---
title: 形式のネゴシエーション
description: 形式のネゴシエーション
ms.assetid: 5b6ee5ed-de5a-4832-a581-179966e79dbd
ms.date: 11/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: d02eedae2c98dcd7b2f46093ed87b2fd20c4c34c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551644"
---
# <a name="format-negotiation"></a>形式のネゴシエーション


アプリケーションは、オーディオ処理を開始すた後、グラフ ビルダーは、オーディオのグラフに、sAPOs を構成し、sAPOs 初期化もします。 オーディオのサービスは、sAPO の入出力にオーディオ データ形式を確立するために LFX sAPO とネゴシエートします。 このネゴシエーション プロセスは、形式のネゴシエーションと呼ばれます。

Windows Vista のオーディオ システム エフェクトを提供するすべての sAPOs は、特定のインターフェイスとメソッドが必要です。 データ形式をネゴシエートする、sAPO とオーディオ エンジンで使用されるメソッドは、: **IsInputFormatSupported**のメソッド、 **IAudioProcessingObject**インターフェイスと**LockForProcess**と**UnlockForProcess**のメソッド、 **IAudioProcessingObjectConfiguration**インターフェイス。 

形式のネゴシエーションを開始するには、オーディオのサービスはまず既定 float32 ベースの形式に LFX sAPO の出力を設定します。 オーディオのサービスを呼び出して、 **IAudioProcessingObject::IsInputFormatSupported** LFX sAPO のメソッドは、既定の形式を提案し、このメソッドの HRESULT の応答を監視します。 返すかどうか、LFX sAPO は推奨される形式をサポートできますが、S\_サポートされている形式への参照と共に、[ok] です。 返すかどうか、LFX sAPO は推奨される形式をサポートできない、S\_候補の 1 つの最も近いと一致する形式への参照と共に FALSE。 APOERR 返します LFX sAPO として推奨される形式をサポートすることはできませんが閉じる一致しない場合は、\_形式\_いない\_サポートされています。 GFX sAPO LFX sAPO の出力形式も連動します。 したがって GFX sAPO は形式のネゴシエーションのプロセスに関与しません。

オーディオ データを処理するデータ形式を選択すると、オーディオ処理のグラフ ビルダーは呼び出し、 **IAudioProcessingObjectConfiguration::LockForProcess**の原因で終了する形式の選択、sAPOs メソッド。

Windows Vista sAPO にエラーへの呼び出しに応答での折り返しのカスタム sAPO を返す場合、 **LockForProcess**メソッド、カスタム sAPO する必要があります、エラーを処理からのエラー処理は**CoCreateInstance** 、sAPO をインスタンス化が試行に失敗するとします。 システム提供の LockForProcess メソッドを上書きする方法の詳細については Spkrfill.cpp ファイルを参照します。

オーディオのサービスが操作する方法のためには、LFX と GFX sAPOs はそれぞれ個別にオーディオ データ形式に関するサービスからのクエリに応答できる必要があります。

**重要な**   Windows Vista LFX sAPO をラップするカスタム sAPO を実装するときに、APO を指定しない\_フラグ\_FRAMESPERSECOND\_する必要があります\_登録の一致フラグカスタム sAPO のプロパティです。 このフラグを指定する場合は、Windows Vista LFX sAPO は塗りつぶしのスピーカー、ヘッドホンによる立体音響仮想化、または仮想サラウンドを実行することできません。 さらに、カスタム、sAPO をダウン ミックス、オーディオ ストリームすることはできません。 たとえば、カスタム、sAPO は 2 チャンネル ステレオ オーディオ ストリームまで 5.1 オーディオ ストリームを混在させることができません。

 

 

 




