---
title: Personal Information Exchange (.pfx) ファイル
description: Personal Information Exchange (.pfx) ファイル
ms.assetid: 58849ccc-c86f-4c49-b848-8926febb5521
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47a5d9fe8dfa02ca0315bd4d8df204eaff27ef4b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532744"
---
# <a name="personal-information-exchange-pfx-files"></a>Personal Information Exchange (.pfx) ファイル


リリースの署名に使用する、ソフトウェア発行元証明書 (SPC)、およびそのプライベートおよびパブリック キーを Personal Information Exchange に格納する必要があります (.*pfx*) ファイル。 ただし、いくつかの証明書機関 (Ca) は、このデータを格納するのにさまざまなファイル形式を使用します。 たとえば、いくつかの Ca が秘密キーで証明書の秘密キーを格納 (.*pvk*) ファイルを開き、証明書と公開キーを格納する *.spc*または *.cer*ファイル。

CA が発行されている場合、 *.spc*以外では、そのキーおよび *.pfx*ファイルを変換し、ファイルを保存、 *.pfx*リリース署名を使用するファイルします。 [ **Pvk2Pfx** ](https://msdn.microsoft.com/library/windows/hardware/ff550672)ツールを使用して、この変換を実行します。

次のコマンドラインの例の変換、 *.pvk*という名前のファイル*abc.pvk*と *.spc*という*abc.spc* に *.pfx*という名前のファイル*abc.pfx*:

```cpp
Pvk2Pfx -pvk abc.pvk -pi pvkpassword -spc abc.spc -pfx abc.pfx -po pfxpassword -f
```

各項目の意味は次のとおりです。

-   **- Pvk**オプションを指定します、 *.pvk*ファイル (*abc.pvk*)。

-   **-Pi**オプションのパスワードを指定します *。pvk*ファイル (*pvkpassword*)。

-   **- Spc**オプションは、名前と証明書を含む SPC ファイルの拡張子を指定します。 ファイルには、いずれかを指定できます、 *.spc*ファイルまたは *.cer*ファイル。 この例で証明書と公開キーが、 *abc.spc*ファイル。

-   **- Pfx**オプションの名前を指定する、 *.pfx*ファイル (*abc.pfx*)。 このオプションが指定されていない場合、Pvk2Pfx は、エクスポート ウィザードを開き、po と f の引数は無視されます。

-   **Po**オプションのパスワードを指定します、 *.pfx*ファイル (*pfxpassword*)。 このオプションが指定されていない場合、指定した *.pfx*ファイルで指定された関連付けられているのと同じパスワードが割り当てられている *.pvk*ファイル。

-   **-F**オプション構成を置き換える既存 Pvk2Pfx *.pfx*ファイルが存在する場合。

SPCs とその管理の詳細については、[ソフトウェア発行元証明書 (SPC)](software-publisher-certificate.md)を参照してください。

 

 





