## 0. make와 makefile이란?

SHELL에서 컴파일을 할 때 

> 참고
>
> http://doc.kldp.org/KoreanDoc/html/GNU-Make/GNU-Make.html#toc7

## 1. 빌드 예제

## 2. makefile 만들기

```
CC			= gcc
CFLAGS		= -Wall -Wextra -Werror
NAME		= libft.a
AR			= ar rcs
RM			= rm -f

# part1
SRCS		=	ft_atoi.c ft_bzero.c ft_calloc.c ft_isalnum.c ft_isalpha.c \
				ft_isascii.c ft_isdigit.c ft_isprint.c ft_memccpy.c ft_memchr.c \
				ft_memcmp.c ft_memcpy.c ft_memmove.c ft_memset.c ft_strchr.c \
				ft_strdup.c ft_strlcat.c ft_strlcpy.c ft_strlen.c ft_strncmp.c \
				ft_strnstr.c ft_strrchr.c ft_tolower.c ft_toupper.c \
# part2
SRCS		+=	ft_substr.c ft_strjoin.c ft_strtrim.c ft_split.c ft_itoa.c \
				ft_strmapi.c ft_putchar_fd.c ft_putstr_fd.c ft_putendl_fd.c ft_putnbr_fd.c \

# bonus part
BOUNUS_SRCS	=	ft_lstnew.c ft_lstadd_front.c ft_lstsize.c ft_lstlast.c ft_lstadd_back.c \
				ft_lstdelone.c ft_lstclear.c ft_lstiter.c ft_lstmap.c

OBJS		= $(SRCS:.c=.o)
BONUS_OBJS	= $(BOUNUS_SRCS:.c=.o)

# .c.o 는 .c파일들과 .o파일을 만든는 확장자 규칙을 정의한다.
# **아래 규칙은 빌드를 할때 .c파일로 생성되는 .o파일의 규칙을 정의한다.**
# $@ 는 현재 목표 파일을 의미한다. [오브젝트파일(.o)들과 대응이 된다.]
# $< 는 현재의 목표 파일보다 더 최근에 갱신된 파일 이름

# $< 는 현재의 목표 파일보다 더 최근에 갱신된 파일 이름이다.
# .o 파일보다 더 최근에 갱신된 .c 파일은 자동적으로 컴파일이 된다.
# 가령 main.o를 만들고 난 다음에 main.c를 갱신하게 되면 main.c는 $<의 작용에 의해 새롭게 컴파일이 된다.
.c.o :
			$(CC) $(CFLAGS) -c $< -o $@

$(NAME):	$(OBJS)
			$(AR) $(NAME) $(OBJS)

all :		$(NAME)

bonus :		$(BONUS_OBJS)
			$(AR) $(NAME) $(BONUS_OBJS)
clean :
			$(RM) $(OBJS) $(BONUS_OBJS)

fclean :		clean
			$(RM) $(NAME)

re :		fclean all

.PHONY :	all bonus clean fclean re

```



1. make 명령어를 치면 우선 makefile에서  `all`규칙이 실행이 된다.
2. `all` 은 `&(NAME)`이라는 규칙을 실행시킨다.
3. `&(NAME)`은 `$(AR) $(NAME) $(OBJS)` 를 실행시킨다.
4. 이때 `OBJS`는 `(SRCS:.c=.o)` 정의되어있어 `SRCS` 에 정의된 파일명들에서 `.c` 가 `.o` 를 대체한 형태를 명시한다.
5. 하지만 오브젝트파일(.o) 파일들이 없으니 오브젝트파일을 생성할 규칙을 찾는다.
6. (`.c.o`  규칙없을때)오브젝트파일을 생성할 규칙이 없으니 ` make` 가 알아서 오브젝트파일을 생성을 시도한다.
7. 그때 `CC`, `CFLAGS` 키워드가 있기 때문에 해당 키워드로 오브젝트 파일을 알아서 생성한다.
8. (.c.o  규칙있을때) `.c.o`  규칙에 따라 c파일들로 오브젝트 파일을 생성한다.
9. (in `NAME`) `ar`  아카이브 명령어를 통해서 생성한 오브젝트 파일들을 이용하여  라이브러리를 생성한다.

