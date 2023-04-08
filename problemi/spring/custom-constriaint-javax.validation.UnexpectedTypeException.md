## Problem, tj greška:

**org.springframework.web.util.NestedServletException: Request processing failed; nested exception is javax.validation.UnexpectedTypeException: HV000030: No validator could be found for constraint 'rs.ac.bg.fon.np.genealogy_spring_boot.member.validation.ValidMemberDto' validating type 'rs.ac.bg.fon.np.genealogy_spring_boot.member.dto.MemberInfoDto'. Check configuration for ''**

Dešava se npr kad neko prosto - predefinisano ograničenje ne može da se primeni na neki tip.

Kod mene se desilo jer sam imao custom ograničenje nad klasom MemberInfoDto a deklarisao sam ga tako da bude primenljivo za MemberSaveDto samo:
     _public class MemberDtoValidator implements ConstraintValidator<ValidMemberDto, MemberSaveDto>_

# Rešenje:

Mora da se napravi novi validator  specijalno za taj tip

**Ali** ne mora nova anotacija, nego mogu u njoj samo da se navedu svi validatori koji je proveravaju

```
@Constraint(validatedBy = {MemberSaveDtoValidator.class, MemberInfoDtoValidator.class})
@Target(ElementType.TYPE)
@Retention(RUNTIME)
public @interface ValidMemberDto {
```
