---
title: パフォーマンスが最適化されたコードのデバッグ
description: パフォーマンスが最適化されたコードのデバッグ
ms.assetid: 9dbae9e7-c181-491e-9566-6f5e8182aae0
keywords:
- パフォーマンスが最適化されたコード
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37dd60ada9fd9760d1a9b46500e49fab16ac69d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571758"
---
# <a name="debugging-performance-optimized-code"></a>パフォーマンスが最適化されたコードのデバッグ


## <span id="ddk_performance_optimized_code_dbg"></span><span id="DDK_PERFORMANCE_OPTIMIZED_CODE_DBG"></span>


マイクロソフトでは、詳細に効率的に実行するようにコンパイルおよびリンクされたコードを再配置に使用される特定の手法があります。 これらの手法では、メモリ階層の場合、コンポーネントを最適化され、トレーニングのシナリオに基づいています。

結果として得られる最適化では、ページング (とページ フォールト) 削減し、コードとデータの間の空間的局所性が向上します。 元のコードの低下を配置し、導入が主要なパフォーマンス ボトルネックに対処します。 この最適化を完了したコンポーネントのバイナリの別の場所に移動関数内で、コードまたはデータのブロックがあります。

これらの手法によって最適化されているモジュールではコードやデータ ブロックの場所は通常のコンパイルとリンクした後はある場所とは異なるメモリ アドレスに多くの場合、確認できます。 さらに、関数可能性がありますに分割されています多くの非連続ブロック、コードの最も一般的に使用されるパスを同じページで、相互に近接配置ことができるようにします。

そのため、関数 (または任意のシンボル) に加えて、オフセットは、最適化されていないコードが同じ意味を必ずしも必要はありません。

### <a name="span-iddebuggingperformanceoptimizedcodespanspan-iddebuggingperformanceoptimizedcodespandebugging-performance-optimized-code"></a><span id="debugging_performance_optimized_code"></span><span id="DEBUGGING_PERFORMANCE_OPTIMIZED_CODE"></span>パフォーマンスが最適化されたコードのデバッグ

デバッグする場合、モジュールがされているかどうかのパフォーマンス最適化を使用して参照できます、 [ **! lmi** ](-lmi.md)シンボルが読み込まれたすべてのモジュールの拡張機能コマンド。

```dbgcmd
0:000> !lmi ntdll
Loaded Module Info: [ntdll]
         Module: ntdll
   Base Address: 77f80000
     Image Name: ntdll.dll
   Machine Type: 332 (I386)
     Time Stamp: 394193d2 Fri Jun 09 18:03:14 2000
       CheckSum: 861b1
Characteristics: 230e stripped perf
Debug Data Dirs: Type Size     VA  Pointer
                 MISC  110,     0,   76c00 [Data not mapped]
     Image Type: DBG      - Image read successfully from symbol server.
                 c:\symbols\dll\ntdll.dbg
    Symbol Type: DIA PDB  - Symbols loaded successfully from symbol server.
                 c:\symbols\dll\ntdll.pdb
```

この出力で、用語に注意してください。 **perf** "特性"行にします。 これは、ntdll.dll をこのパフォーマンスの最適化が適用されたことを示します。

デバッガーが関数または;、オフセットを持たない他のシンボルを理解できます。これにより、関数または他のラベルは問題なくでブレークポイントを設定することができます。 ただし、逆アセンブル操作の出力を混乱を招くため、この逆アセンブル、オプティマイザーによって行われた変更が反映されますがあります。

デバッガーは、元のコードの近くに維持しようと、ため愉快な結果が表示されます。 原則として、パフォーマンスが最適化されたコードを使用する場合は、単に最適化されたコードの信頼性の高いアドレス算術演算を実行することはできません。

以下に例を示します。

```dbgcmd
kd> bl
 0 e f8640ca6     0001 (0001) tcpip!IPTransmit
 1 e f8672660     0001 (0001) tcpip!IPFragment

kd> u f864b4cb
tcpip!IPTransmit+e48:
f864b4cb f3a4             rep     movsb
f864b4cd 8b75cc           mov     esi,[ebp-0x34]
f864b4d0 8b4d10           mov     ecx,[ebp+0x10]
f864b4d3 8b7da4           mov     edi,[ebp-0x5c]
f864b4d6 8bc6             mov     eax,esi
f864b4d8 6a10             push    0x10
f864b4da 034114           add     eax,[ecx+0x14]
f864b4dd 57               push    edi
```

ブレークポイントから確認できますを一覧表示のアドレス**IPTransmit** 0xF8640CA6 です。

0xF864B4CB でこの関数内でコードのセクションを逆アセンブルするときに、関数の先頭を超えて 0xE48 バイトである出力を示します。 ただし、このアドレスからの関数の基本を減算する場合は、0xA825 する実際のオフセットが表示されます。

これは、何が起こっているか。デバッガーは、0xF864B4CB で始まるバイナリ命令の逆アセンブリを実際に表示されています。 単純な減算して、オフセットを計算する代わりにデバッガーを表示する--可能な--最適化が実行される前に、元のコードでほど関数のエントリのオフセットが存在して最善策として。 値が 0xE48 であります。

その一方で見てしようとする場合に**IPTransmit**+ 0xE48、これが表示されます。

```dbgcmd
kd> u tcpip!iptransmit+e48
tcpip!ARPTransmit+d8:
f8641aee 0856ff           or      [esi-0x1],dl
f8641af1 75fc             jnz     tcpip!ARPTransmit+0xd9 (f8641aef)
f8641af3 57               push    edi
f8641af4 e828eeffff       call    tcpip!ARPSendData (f8640921)
f8641af9 5f               pop     edi
f8641afa 5e               pop     esi
f8641afb 5b               pop     ebx
f8641afc c9               leave
```

ここでは、デバッガーがシンボルを認識している何が起きている**IPTransmit** 0xF8640CA6、アドレスに相当し、コマンドとしてパーサーはその 0xF8640CA6 + 0xE48 = 0xF8641AEE を検索する単純な加算を実行します。 このアドレスは、引数として使用し、 [ **u (Unassemble)** ](u--unassemble-.md)コマンド。 デバッガーはないことを検出したら、この場所が分析される場合が**IPTransmit** plus 0xE48 のオフセット。 実際、一部ではないこの関数のすべての。 関数に対応する代わりに、 **ARPTransmit** plus 0xD8 のオフセット。

このような理由では、そのパフォーマンスの最適化は、アドレス算術演算を元に戻すことはできません。 デバッガーは、アドレスを取得し、元のシンボルとオフセットを推測、シンボルを取得し、オフセットし、正しいアドレスに変換するために必要な情報がありません。 そのため、逆アセンブリでは、このような場合役に立ちません。

 

 





