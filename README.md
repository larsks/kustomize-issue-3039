This is an example to accompany [kubernetes-sigs/kustomize#3039][].

[kubernetes-sigs/kustomize#3039]: https://github.com/kubernetes-sigs/kustomize/issues/3039

This works:

```
$  kustomize build works | grep memberlist
  name: memberlist-8f765gmmdh
              name: memberlist-8f765gmmdh
```

This fails:

```
$ kustomize build fails | grep memberlist
  name: memberlist-8f765gmmdh
              name: memberlist
```

The only difference between the two configurations:

```
diff -ruN fails/metallb.yml works/metallb.yml
--- fails/metallb.yml	2020-09-25 13:25:45.399570824 -0400
+++ works/metallb.yml	2020-09-25 13:26:28.593535470 -0400
@@ -3,7 +3,6 @@
 kind: DaemonSet
 metadata:
   name: speaker
-  namespace: metallb-system
 spec:
   selector:
     matchLabels:
```
