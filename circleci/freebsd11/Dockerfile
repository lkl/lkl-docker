ARG IMAGE_NAME

FROM $IMAGE_NAME
# As of June 2023, freebsd pkg site, http://pkg.FreeBSD.org/FreeBSD:11:amd64/quarterly/
# is no longer available.  We currently have no plan to update FreeBSD support,
# so, we reuse existing image, from 0.4 tag, to create newer images.
# If we will update FreeBSD version of support, revert this commit and
# rewrite the relevant part of scripts.
FROM lkldocker/circleci-freebsd11-x86_64:0.4
LABEL authors="Hajime Tazaki <thehajime@gmail.com>"

