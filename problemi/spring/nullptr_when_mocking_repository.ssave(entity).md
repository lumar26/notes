###Problem: 

Javljala se greška akd treba da mokujem čuvanje u bazi nekog entiteta:

`Mockito.when(memberRepository.save(member)).thenReturn(member);`

dobija se greška: 

```
java.lang.NullPointerException
	at rs.ac.bg.fon.np.genealogy_spring_boot.model.dto.response.MemberBasicInfoResponse.of(MemberBasicInfoResponse.java:35)
	at rs.ac.bg.fon.np.genealogy_spring_boot.service.impl.MemberServiceImpl.saveMember(MemberServiceImpl.java:70)
```

### Rešenje:
        Mockito.when(memberRepository.save(any(Member.class))).thenReturn(member);
gde je **any** metoda iz `ArgumentMatchers`

