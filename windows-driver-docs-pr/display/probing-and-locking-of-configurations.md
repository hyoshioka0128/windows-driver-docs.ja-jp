---
title: プローブと構成のロック
description: プローブと構成のロック
ms.assetid: 6f68db48-ed4b-487c-b425-43c610651c16
keywords:
- ビデオのデコード WDK DirectX va なので、構成のプローブとロック
- ビデオの WDK DirectX va なので、構成のプローブとロックのデコード
- WDK の DirectX va なので、構成のプローブとロックをデコードする画像
- 最小限の相互運用性の構成設定の WDK DirectX VA
- ロック構成 WDK DirectX VA
- WDK DirectX VA の構成のプローブ
- 構成のプローブと WDK DirectX VA のロック
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d31d21d387fdbfacaab9fbe22cf2043d2f12b8cf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550844"
---
# <a name="probing-and-locking-of-configurations"></a>プローブと構成のロック


## <span id="ddk_probing_and_locking_of_configurations_gg"></span><span id="DDK_PROBING_AND_LOCKING_OF_CONFIGURATIONS_GG"></span>


各 DirectX VA 関数の構成を確立するためのプロセス (特定の値の[bDXVA\_Func](bdxva-func-variable.md)) を構成する必要があります (画像をデコード、アルファ ブレンドのデータの読み込み中に、たとえば、圧縮とアルファ ブレンドの組み合わせ) で実行できます。

1.  アクセラレータで、構成を受け入れるかどうかを判断する (必要な場合) を調査します。

2.  サポートされている場合は、固有の構成でロックします。

プローブのコマンドが、特定のアクセラレータに送信される特定の構成がサポートされている場合を判断する*bDXVA\_Func*構成と共に、広範囲の値。 プローブのコマンドでは、構成構造体だけでなく (の値に*bDXVA\_Func*) 構成がサポートされているかどうかを判断するプローブされている構成について説明しますが送信されます。 アクセラレータは、秒の値を返します\_OK] または [S\_アクセラレータで指定された構成がサポートされているかどうかを示す FALSE。 アクセラレータでは、推奨される代替の構成を返すこともできます。

固有の構成でロック、ロックのコマンドは、特定のアクセラレータに送信*bDXVA\_Func*をロックできます。 ロックのコマンドでは、構成構造 (の値に*bDXVA\_Func*) 構成がサポートされている場合、構成をロックするについて説明しますが送信されます。 アクセラレータは、秒を返します\_OK] または [S\_FALSE、アクセラレータで指定された構成がサポートされているかどうかを示します。 場合、戻り値は S\_使用するため、指定した構成がロックされて、します。 場合、戻り値は S\_false の場合、推奨される代替の構成が返されます。

デコーダーは、最初に指定された構成のプローブのコマンドを送信せずにロック コマンドを送信することがあります。 アクセラレータが S を返す場合\_S を返しますが、特定の構成のプローブ コマンドは、ok\_断りのない限り、その同じ構成では、ロック コマンドに ok をクリックします。 ロック コマンドが送信され、アクセス キーを返します後 S\_で指定された構成がロックされているし、追加の調査やロック コマンドは送信されません、デコーダーの同じ値の*bDXVA\_Func*.

すべての DirectX VA ソフトウェア デコーダーはすべての DirectX VA アクセラレータで行えることを確認する、[最小限の相互運用性の構成セット](minimal-interoperability-configuration-sets.md)構成が特定を使用して、デコーダーでサポートする必要がありますのセットとして定義されます場合は値*bDXVA\_Func*します。 すべてのアクセラレータのサポートを示す、 *bDXVA\_Func*関連のビデオ アクセラレータを公開することで変数の GUID はこの相互運用性の構成セットの 1 つ以上のメンバーをサポートする必要があります。 場合によってで、[追加の推奨構成セット](additional-encouraged-configuration-set.md)も定義されている可能性があります。

次の図は、プローブと、デコーダーによって送信されたコマンドのロックの制御フローを示します。

![プローブとドライバーの構成を設定するロックを示すフローチャート](images/probe-lock.png)

 

 





